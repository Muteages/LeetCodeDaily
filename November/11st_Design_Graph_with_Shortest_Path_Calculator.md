# Design Graph with Shortest Path Calculator

https://leetcode.com/problems/design-graph-with-shortest-path-calculator

There is a directed weighted graph that consists of n nodes numbered from 0 to n - 1. The edges of the graph are initially represented by the given array edges where edges[i] = [fromi, toi, edgeCosti] meaning that there is an edge from fromi to toi with the cost edgeCosti.

Implement the Graph class:

Graph(int n, int[][] edges) initializes the object with n nodes and the given edges.
addEdge(int[] edge) adds an edge to the list of edges where edge = [from, to, edgeCost]. It is guaranteed that there is no edge between the two nodes before adding this one.
int shortestPath(int node1, int node2) returns the minimum cost of a path from node1 to node2. If no path exists, return -1. The cost of a path is the sum of the costs of the edges in the path.

## Approach 

Dijkstra
``` C++
std::vector<std::vector<std::pair<int, int>>> graph; // next node - edge cost
public:
    Graph(int n, vector<vector<int>>& edges)
    {
        graph.resize(n);
        for (auto& edge : edges)
        {
            addEdge(edge);
        }
    }
    
    inline void addEdge(vector<int> edge) {
        int start = edge[0];
        int end = edge[1];
        int cost = edge[2];
        graph[start].emplace_back(end, cost);
    }
    
    int shortestPath(int node1, int node2) {
        std::vector<int> minCost(graph.size(), INT_MAX);
        minCost[node1] = 0;

        std::priority_queue<std::pair<int, int>, std::vector<std::pair<int, int>>, std::greater<>> pq; // the cost to reach current node- current node
        pq.emplace(0, node1);

        while (!pq.empty())
        {
            auto [cost, node] = pq.top();
            pq.pop();

            if (cost > minCost[node])
            {
                continue;
            }

            if (node == node2)
            { // Find the node
                return cost;
            }

            for (auto& [next, nextCost] : graph[node])
            {
                int tempCost = nextCost + cost;
                if (tempCost < minCost[next])
                {
                    minCost[next] = tempCost;
                    pq.emplace(tempCost, next);
                }
            }
        }
        return -1;
    }
```