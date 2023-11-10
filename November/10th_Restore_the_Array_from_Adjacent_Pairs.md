# Restore the Array from Adjacent Pairs

https://leetcode.com/problems/restore-the-array-from-adjacent-pairs

There is an integer array nums that consists of n unique elements, but you have forgotten it. However, you do remember every pair of adjacent elements in nums.

You are given a 2D integer array adjacentPairs of size n - 1 where each adjacentPairs[i] = [ui, vi] indicates that the elements ui and vi are adjacent in nums.

It is guaranteed that every adjacent pair of elements nums[i] and nums[i+1] will exist in adjacentPairs, either as [nums[i], nums[i+1]] or [nums[i+1], nums[i]]. The pairs can appear in any order.


## Approach 1
``` C++
    vector<int> restoreArray(vector<vector<int>>& adjacentPairs) {
        std::unordered_map<int, std::vector<int>> adjacent; // node - adjacent nodes
        for (auto& pair : adjacentPairs)
        {
            int n1 = pair[0];
            int n2 = pair[1];
            adjacent[n1].emplace_back(n2);
            adjacent[n2].emplace_back(n1);
        } 

        // Find the head
        int curr = 0;
        for (auto& [node, adj] : adjacent)
        {
            if (adj.size() == 1)
            {
                curr = node;
                break;
            }
        }

        std::vector<int> ans;
        ans.emplace_back(curr);
        std::set<int> visited;
        visited.insert(curr);
        while (ans.size() != adjacent.size())
        {
            for (auto next : adjacent[curr])
            {
                if (!visited.count(next))
                { // Find an unvisited node as next node
                    ans.emplace_back(next);
                    visited.insert(next);
                    curr = next;
                    break;
                }
            }
        }
        return ans;
    }
```

## Approach 2
Avoid visited array by using a "previous" variable

``` C++
    vector<int> restoreArray(vector<vector<int>>& adjacentPairs) {
        // Same with A1
        std::vector<int> ans;
        ans.emplace_back(curr);
        int prev = INT_MAX;
        while (ans.size() != adjacent.size())
        {
            for (auto next : adjacent[curr])
            {
                if (next != prev)
                {
                    ans.emplace_back(next);
                    prev = curr;
                    curr = next;
                    break;
                }
            }
        }
        return ans;
    }
```

## Approach 3

DFS

``` C++
private: 
    std::unordered_map<int, std::vector<int>> adjacent; // node - adjacent nodes
    std::set<int> visited;
    std::vector<int> ans;
    void dfs(int node)
    {   
        if (visited.count(node))
        {
            return;
        }

        ans.emplace_back(node);
        visited.insert(node);
        for (auto next : adjacent[node])
        {
            dfs(next);
        }
    }
public:
    vector<int> restoreArray(vector<vector<int>>& adjacentPairs) {
        for (auto& pair : adjacentPairs)
        {
            int n1 = pair[0];
            int n2 = pair[1];
            adjacent[n1].emplace_back(n2);
            adjacent[n2].emplace_back(n1);
        } 

        // Find the head
        int curr = 0;
        for (auto& [node, adj] : adjacent)
        {
            if (adj.size() == 1)
            {
                curr = node;
                break;
            }
        }
        dfs(curr);
        return ans;
    }
```


