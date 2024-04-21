# Find if Path Exists in Graph

https://leetcode.com/problems/find-if-path-exists-in-graph

There is a bi-directional graph with n vertices, where each vertex is labeled from 0 to n - 1 (inclusive). The edges in the graph are represented as a 2D integer array edges, where each edges[i] = [ui, vi] denotes a bi-directional edge between vertex ui and vertex vi. Every vertex pair is connected by at most one edge, and no vertex has an edge to itself.

You want to determine if there is a valid path that exists from vertex source to vertex destination.

Given edges and the integers n, source, and destination, return true if there is a valid path from source to destination, or false otherwise.

## Approach 1


BFS

``` C++
class Solution {
public:
    bool validPath(int n, vector<vector<int>>& edges, int source, int destination) {
        if (source == destination)
        {
            return true;
        }
        std::vector<std::vector<int>> graph(n);
        for (const auto& edge : edges)
        {
            graph[edge[0]].emplace_back(edge[1]);
            graph[edge[1]].emplace_back(edge[0]);
        }
        std::vector<bool> visited(n, false);
        std::queue<int> bfs;
        bfs.emplace(source);
        visited[source] = true;
        while (!bfs.empty())
        {
            int curr = bfs.front();
            bfs.pop();
            if (curr == destination)
            {
                return true;
            }
            for (int next : graph[curr])
            {
                if (!visited[next])
                {
                    bfs.emplace(next);
                    visited[next] = true;
                }
            }
        }
        return false;
    }
};
```

## Approach 2

DFS but very slow

``` C++
    bool dfs(std::vector<std::vector<int>>& graph, std::vector<bool>& visited, int source, const int destination)
    {
        if (source == destination)
        {
            return true;
        }
        visited[source] = true;
        for (int next : graph[source])
        {
            if (!visited[next])
            {
                if (dfs(graph, visited, next, destination))
                {
                    return true;
                }
            }
        }
        return false;
    }


    bool validPath(int n, vector<vector<int>>& edges, int source, int destination) {
        if (source == destination)
        {
            return true;
        }
        std::vector<std::vector<int>> graph(n);
        std::vector<bool> visited(n, false);
        for (const auto& edge : edges)
        {
            graph[edge[0]].emplace_back(edge[1]);
            graph[edge[1]].emplace_back(edge[0]);
        }
        return dfs(graph, visited, source, destination);
    }
```