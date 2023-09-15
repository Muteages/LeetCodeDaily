# Min Cost to Connect All Points

https://leetcode.com/problems/min-cost-to-connect-all-points/description/

You are given an array points representing integer coordinates of some points on a 2D-plane, where points[i] = [xi, yi].

The cost of connecting two points [xi, yi] and [xj, yj] is the manhattan distance between them: |xi - xj| + |yi - yj|, where |val| denotes the absolute value of val.

Return the minimum cost to make all points connected. All points are connected if there is exactly one simple path between any two points.


## Approach 1

Prim's Algorithm to find the MST

``` C++
    int minCostConnectPoints(vector<vector<int>>& points) {

        int n = points.size();
        std::vector<bool> visited(n, false);
        std::priority_queue<std::pair<int, int>, std::vector<std::pair<int, int>>, std::greater<std::pair<int, int>>> pq; // weight - node
        pq.push({0, 0});
        int cost = 0;
        int remaining = n; // Nodes are prepared to connected
        while (remaining > 0)
        {
            auto [weight, node] = pq.top(); // Get minimum weight
            pq.pop();

            if (!visited[node])
            {
                visited[node] = true;
                cost += weight;
                remaining--;

                for (int connectedNode = 0; connectedNode < n; connectedNode++)
                { 
                    if (!visited[connectedNode])
                    {   // Calculate the dis with the rest of unvisited nodes
                        int w = std::abs(points[node][0] - points[connectedNode][0]) + std::abs(points[node][1] - points[connectedNode][1]);
                        pq.push({w, connectedNode});
                    }
                }
            }
        }
        return cost;
    }
```