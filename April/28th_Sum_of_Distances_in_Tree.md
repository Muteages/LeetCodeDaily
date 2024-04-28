# Sum of Distances in Tree

https://leetcode.com/problems/sum-of-distances-in-tree

There is an undirected connected tree with n nodes labeled from 0 to n - 1 and n - 1 edges.

You are given the integer n and the array edges where edges[i] = [ai, bi] indicates that there is an edge between nodes ai and bi in the tree.

Return an array answer of length n where answer[i] is the sum of the distances between the ith node in the tree and all other nodes.


## Approach

``` C++
    std::vector<std::vector<int>> graph;
    std::vector<int> cnt;
    std::vector<int> sum;

    void dfs(int curr, int parent)
    {
        for (int child : graph[curr])
        {
            if (parent != child)
            {
                dfs(child, curr);
                cnt[curr] += cnt[child];
                sum[curr] += sum[child] + cnt[child];
            }
        }
    }

    void reRoot(int curr, int parent)
    {
        for (int child : graph[curr])
        {
            if (parent != child)
            {
                sum[child] = sum[curr] - cnt[child] + (cnt.size() - cnt[child]);
                reRoot(child, curr);
            }
        }
    }

    vector<int> sumOfDistancesInTree(int n, vector<vector<int>>& edges) {
        cnt.assign(n, 1);
        sum.assign(n, 0);
        graph.resize(n);
        for (const auto& edge: edges)
        {
            graph[edge[0]].emplace_back(edge[1]);
            graph[edge[1]].emplace_back(edge[0]);
        }

        dfs(0, -1);
        reRoot(0, -1);
        return sum;
    }
```