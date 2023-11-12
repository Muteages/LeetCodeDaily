# Bus Routes

https://leetcode.com/problems/bus-routes

You are given an array routes representing bus routes where routes[i] is a bus route that the ith bus repeats forever.

For example, if routes[0] = [1, 5, 7], this means that the 0th bus travels in the sequence 1 -> 5 -> 7 -> 1 -> 5 -> 7 -> 1 -> ... forever.
You will start at the bus stop source (You are not on any bus initially), and you want to go to the bus stop target. You can travel between bus stops by buses only.

Return the least number of buses you must take to travel from source to target. Return -1 if it is not possible.

## Approach 1

BFS 

``` C++
    int numBusesToDestination(vector<vector<int>>& routes, int source, int target) {
        if (source == target)
        {
            return 0;
        }

        std::unordered_map<int, std::vector<int>> stops; // stops - available buses at current stop
        for (int i = 0; i < routes.size(); i++)
        {
            for (auto& stop : routes[i])
            {
                stops[stop].emplace_back(i);
            }
        }

        if (stops.find(source) == stops.end() || stops.find(target) == stops.end())
        { // No target or source in the provided stop list
            return -1;
        }

        std::queue<int> candidates; // stop candidate
        candidates.emplace(source);

        std::set<int> visitedBus;
        std::set<int> visitedStop;
        int busCnt = 0;
        
        while (!candidates.empty())
        {
            busCnt++;
            int stopNum = candidates.size();
            for (int i = 0; i < stopNum; i++)
            {
                int stop = candidates.front();
                candidates.pop();
                for (const auto& bus : stops[stop])
                {
                    if (visitedBus.count(bus))
                    { // Pass if the bus has been visited
                        continue;
                    }
                    visitedBus.insert(bus);
                    for (const auto& nextStop : routes[bus])
                    {
                        if (nextStop == target)
                        { // Find the target
                            return busCnt;
                        }

                        if (visitedStop.count(nextStop))
                        { // Pass if the stop has been visited
                            continue;
                        }
                        visitedStop.insert(nextStop);
                        candidates.emplace(nextStop);
                    }
                }
            }            
        }
        return -1;
    }
```

## Approach 2

``` C++
    int numBusesToDestination(vector<vector<int>>& routes, int source, int target) {
        if (source == target)
        {
            return 0;
        }

        int maxStop = -1;
        for (const auto& route : routes)
        {
            for (const auto& stop : route)
            {
                maxStop = std::max(maxStop, stop);
            }
        }

        std::vector<int> minBusCnt(maxStop + 1, INT_MAX); // Minimum bus number to reach current stop
        minBusCnt[source] = 0;

        int updated = true;
        while (updated)
        {
            updated = false;
            for (const auto& route : routes)
            {
                int curMin = routes.size() + 1;
                for (const auto& stop : route)
                {
                    curMin = std::min(curMin, minBusCnt[stop]);
                }

                curMin++;
                for (const auto& stop : route)
                {
                    if (curMin < minBusCnt[stop])
                    {
                        minBusCnt[stop] = curMin;
                        updated = true;
                    }
                }
            }
        }

        return (minBusCnt[target] >= routes.size() + 1) ? -1 : minBusCnt[target];
    }
```