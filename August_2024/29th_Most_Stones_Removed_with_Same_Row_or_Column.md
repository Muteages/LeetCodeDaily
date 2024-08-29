# Most Stones Removed with Same Row or Column

https://leetcode.com/problems/most-stones-removed-with-same-row-or-column

On a 2D plane, we place n stones at some integer coordinate points. Each coordinate point may have at most one stone.

A stone can be removed if it shares either the same row or the same column as another stone that has not been removed.

Given an array stones of length n where stones[i] = [xi, yi] represents the location of the ith stone, return the largest possible number of stones that can be removed.

## Approach

Instead of calculating how many stones can be removed, we can calculate how many connected paths we can gather in the graph. For each path, we can remove path.length - 1 stones.

``` C++
class Solution {
public:
    void dfs(const vector<vector<int>>& stones, const vector<vector<int>>& rows, const vector<vector<int>>& cols, std::bitset<1001>& visited, int idx)
    {
        if (visited[idx]) return;

        visited.flip(idx);
        int row = stones[idx][0], col = stones[idx][1];
        for (const auto& r : rows[row])
        {
            dfs(stones, rows, cols, visited, r);
        }
        for (const auto& c : cols[col])
        {
            dfs(stones, rows, cols, visited, c);
        }
    }

    int removeStones(vector<vector<int>>& stones) {
        const int n = stones.size();
        if (n == 1) return 0;
        std::vector<std::vector<int>> rows(10001), cols(10001);
        for (int i = 0; i < n; i++)
        {
            int row = stones[i][0], col = stones[i][1];
            rows[row].emplace_back(i);
            cols[col].emplace_back(i);
        }

        int connects = 0;
        std::bitset<1001> visited{};
        for (int i = 0; i < n; i++)
        {
            int row = stones[i][0], col = stones[i][1];
            if (!visited[i])
            {
                dfs(stones, rows, cols, visited, i);
                connects++;
            }
        }
        return n - connects;
    }
};
```

``` JavaScript
var removeStones = function(stones) {
    const n = stones.length;
    const vis = new Set();
    const rows = Array.from({ length: 10001 }, () => []);
    const cols = Array.from({ length: 10001 }, () => []);
    for (let [r, c] of stones) {
        rows[r].push(c);
        cols[c].push(r);
    }

    const dfs = (r, c) => {
        const key = `${r}-${c}`; 
        if (vis.has(key)) return;
        vis.add(key);
        for (let col of rows[r]) {
            dfs(r, col);
        }
        for (let row of cols[c]) {
            dfs(row, c);
        }
    };

    let connects = 0;
    for (let [r, c] of stones) {
        const key = `${r}-${c}`;
        if (!vis.has(key)) {
            dfs(r, c);
            connects++;
        }
    }
    return n - connects;
};
```