# Minimum Height Trees

https://leetcode.com/problems/minimum-height-trees/

A tree is an undirected graph in which any two vertices are connected by exactly one path. In other words, any connected graph without simple cycles is a tree.

Given a tree of n nodes labelled from 0 to n - 1, and an array of n - 1 edges where edges[i] = [ai, bi] indicates that there is an undirected edge between the two nodes ai and bi in the tree, you can choose any node of the tree as the root. When you select a node x as the root, the result tree has height h. Among all possible rooted trees, those with minimum height (i.e. min(h))  are called minimum height trees (MHTs).

Return a list of all MHTs' root labels. You can return the answer in any order.


## Approach 1

Brute force. TLE for large cases
```C++
   vector<int> findMinHeightTrees(int n, vector<vector<int>>& edges) {
        std::vector<int> mhts;
        int minHeight = INT_MAX;
        std::vector<std::vector<int>> graph(n);
        for (int i = 0; i < edges.size(); i++)
        {
            int src = edges[i][0], des = edges[i][1];
            graph[src].emplace_back(des);
            graph[des].emplace_back(src);
        }
        for (int i = 0; i < n; i++)
        {
            std::queue<std::pair<int, int>> bfs; // node - current height
            bfs.emplace(i, 0);
            std::vector<bool> visited(n, false);
            visited[i] = true;
            int curHeight = 0;
            while (!bfs.empty())
            {
                auto [curr, height] = bfs.front();
                bfs.pop();
                for (int next : graph[curr])
                {
                    if (!visited[next])
                    {
                        bfs.emplace(next, height + 1);
                        visited[next] = true;
                        curHeight = std::max(curHeight, height + 1);
                    }
                }                
            }    
            if (curHeight == minHeight)
            {
                mhts.emplace_back(i);
            }
            else if (curHeight < minHeight)
            {
                mhts.clear();
                mhts.emplace_back(i);
                minHeight = curHeight;
            }
        }
        return mhts;
    }
```

## Approach 2

Optimal approach: deleting all current leaf node in every iteration. the remaining nodes are the roots of the MHTs.

```C++
    vector<int> findMinHeightTrees(int n, vector<vector<int>>& edges) {
        if (n == 1)
        {
            return {0};
        }
        std::vector<int> mhts;
        std::vector<int> deg(n, 0);
        std::vector<std::vector<int>> graph(n);
        for (const auto& edge : edges)
        {
            int src = edge[0], des = edge[1];
            graph[src].emplace_back(des);
            graph[des].emplace_back(src);
            deg[src]++;
            deg[des]++;
        }

        std::queue<int> bfs;
        for (int i = 0; i < n; i++)
        {
            if (deg[i] == 1)
            { // Leaf node
                bfs.emplace(i);
            }
        }

        while (!bfs.empty())
        {
            int sz = bfs.size();
            n -= sz; // Remaining nodes
            for (int i = 0; i < sz; i++)
            {
                int curr = bfs.front();
                bfs.pop();
                if (n == 0)
                {
                    mhts.emplace_back(curr);
                }
                for (const int next : graph[curr])
                {
                    if (--deg[next] == 1)
                    {
                        bfs.emplace(next);
                    }
                }
            }
        }
        return mhts;
    }
```