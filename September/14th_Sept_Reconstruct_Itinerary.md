# Reconstruct Intinerary

https://leetcode.com/problems/reconstruct-itinerary/description

You are given a list of airline tickets where tickets[i] = [fromi, toi]

All of the tickets belong to a man who departs from "JFK", thus, the itinerary must begin with "JFK". If there are multiple valid itineraries, you should return the itinerary that has the smallest lexical order when read as a single string.

## Approach 1

Revursive way

``` C++
    vector<string> findItinerary(vector<vector<string>>& tickets) {   
        std::unordered_map<std::string, std::vector<std::string>> graph; // start - end list

        for (auto& ticket : tickets)
        { // Initialise the graph
            graph[ticket[0]].emplace_back(ticket[1]);
        }

        for (auto& [start, endList] : graph)
        { // Create the lexical order
            std::sort(endList.begin(), endList.end(), std::greater<std::string>());
        }

        std::vector<std::string> itinerary;

        std::function<void(const std::string&)> dfs = [&](const std::string& start)
        {
            while (!graph[start].empty())
            {
                std::string next = graph[start].back();
                graph[start].pop_back();
                dfs(next);
            }
            itinerary.emplace_back(start);
        };

        dfs("JFK");
        std::reverse(itinerary.begin(), itinerary.end());
        return itinerary; 
    }
```


## Approach 2 

Iterative way

``` C++
   vector<string> findItinerary(vector<vector<string>>& tickets) {   
        std::unordered_map<std::string, std::vector<std::string>> graph; // start - end list

        for (auto& ticket : tickets)
        { // Initialise the graph
            graph[ticket[0]].emplace_back(ticket[1]);
        }

        for (auto& [start, endList] : graph)
        { // Create the lexical order
            std::sort(endList.begin(), endList.end(), std::greater<std::string>());
        }

        std::vector<std::string> itinerary;
        std::stack<std::string> dfs;
        dfs.emplace("JFK");

        while (!dfs.empty())
        {
            std::string curr = dfs.top();
            if (!graph[curr].empty())
            {
                dfs.emplace(graph[curr].back());
                graph[curr].pop_back();
            }
            else
            {
                itinerary.emplace_back(dfs.top());
                dfs.pop();
            }
        }

        std::reverse(itinerary.begin(), itinerary.end());
        return itinerary; 
    }
```