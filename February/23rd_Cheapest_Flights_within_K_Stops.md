# Cheapest Flights Within K Stops

https://leetcode.com/problems/cheapest-flights-within-k-stops

There are n cities connected by some number of flights. You are given an array flights where flights[i] = [fromi, toi, pricei] indicates that there is a flight from city fromi to city toi with cost pricei.

You are also given three integers src, dst, and k, return the cheapest price from src to dst with at most k stops. If there is no such route, return -1.

## Approach 

``` C++
    int findCheapestPrice(int n, vector<vector<int>>& flights, int src, int dst, int k) {
        std::vector<std::vector<std::pair<int, int>>> m(101); // from index i to p1, price is p2
        for (const auto& flight : flights)
        {
            m[flight[0]].emplace_back(flight[1], flight[2]);
        }

        int ans = INT_MAX;
        std::queue<std::pair<int, int>> q;  // airport - current total price
        std::vector<int> minPrice(101, INT_MAX); // Record current price at each stop airport
        q.emplace(src, 0);
        while (!q.empty() && k-- >= 0)
        {
            int n = q.size();
            while (n--)
            {
                auto [curr, prevTotal] = q.front(); 
                q.pop();
                for (const auto& [next, price] : m[curr])
                {
                    if (prevTotal + price < minPrice[next])
                    { // Only visit next nodes if the new total price is cheaper
                        minPrice[next] = prevTotal + price;
                        if (src != next)
                        { // No need to visit following nodes of destination
                            q.emplace(next, minPrice[next]);
                        }
                    }
                }
            }
        }
        return minPrice[dst] == INT_MAX ? -1 : minPrice[dst];
    }
```