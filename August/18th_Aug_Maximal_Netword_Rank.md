# Maximal Network Rank

https://leetcode.com/problems/maximal-network-rank/description/

There is an infrastructure of n cities with some number of roads connecting these cities. Each roads[i] = [ai, bi] indicates that there is a bidirectional road between cities ai and bi.

The network rank of two different cities is defined as the total number of directly connected roads to either city. If a road is directly connected to both cities, it is only counted once.

The maximal network rank of the infrastructure is the maximum network rank of all pairs of different cities.

Given the integer n and the array roads, return the maximal network rank of the entire infrastructure.


## Approach 1

Record each city's connections and then find two max numbers. Reduce one if they are connected.

``` C++
    int maximalNetworkRank(int n, vector<vector<int>>& roads) {
        std::vector<int> connections(n); // city - connections 
        std::set<std::pair<int, int>> pairs; // store city pairs if they are connected
        for (auto& road : roads)
        {
            int city1 = road[0];
            int city2 = road[1];

            connections[city1]++;
            connections[city2]++;

            pairs.insert({city1, city2});
            pairs.insert({city2, city1});
        }

        int maxRank = 0;

        for (int i = 0; i < n; i++)
        {
            for (int j = i + 1; j < n; j++)
            {
                int curRank = connections[i] + connections[j];
                if (pairs.count({i, j}))
                { // if tow cities are connected
                    curRank--;
                }
                maxRank = std::max(maxRank, curRank);
            }
        }

        return maxRank;
    }
```


## Approach 2 

``` C++
    int maximalNetworkRank(int n, vector<vector<int>>& roads) {
        vector<unordered_set<int>> connections(n); // store each city's adiacent cities. i.e the connections

        for (auto& road : roads)
        {
            connections[road[0]].insert(road[1]);
            connections[road[1]].insert(road[0]);
        }

        int maxRank = 0;
        for (int i = 0; i < n; i++)
        {
            for (int j = i + 1; j < n; j++)
            {
                int currentRank = connections[i].size() + connections[j].size();
                if (connections[i].count(j))
                { // if two cities are connected
                    currentRank--;
                }
                maxRank = std::max(maxRank, currentRank);
            }
        }
        return maxRank;
    }
```