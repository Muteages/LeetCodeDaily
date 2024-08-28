# Count Sub-Islands

https://leetcode.com/problems/count-sub-islands

You are given two m x n binary matrices grid1 and grid2 containing only 0's (representing water) and 1's (representing land). An island is a group of 1's connected 4-directionally (horizontal or vertical). Any cells outside of the grid are considered water cells.

An island in grid2 is considered a sub-island if there is an island in grid1 that contains all the cells that make up this island in grid2.

Return the number of islands in grid2 that are considered sub-islands.


## Approach 

``` C++
    std::pair<int, int> dir[4] = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};
    int m{}, n{};
    bool isSubland(std::vector<std::vector<int>>& grid1, std::vector<std::vector<int>>& grid2, int r, int c)
    {
        if (r < 0 || r >= m || c < 0 || c >= n || grid2[r][c] != 1) return true;
        if (grid1[r][c] != 1) return false;

        grid2[r][c] = 2; // Set as visited
        bool isSub = true;
        for (const auto& [dr, dc] : dir)
        {
            int row = r + dr, col = c + dc;
            isSub &= isSubland(grid1, grid2, row, col);
        }
        return isSub;
    }
    int countSubIslands(vector<vector<int>>& grid1, vector<vector<int>>& grid2) {
        m = grid1.size(), n = grid1[0].size();
        int ans = 0;
        for (int r = 0; r < m; r++)
        {
            for (int c = 0; c < n; c++)
            {
                if (grid2[r][c] == 1)
                {
                    ans += isSubland(grid1, grid2, r, c);
                }
            }
        }
        return ans;
    }
```

``` JavaScript
var countSubIslands = function(grid1, grid2) {
    const m = grid1.length, n = grid1[0].length;
    let dir = [[0, 1], [0, -1], [1, 0], [-1, 0]];
    const isSubland = (r, c) => {
        if (r < 0 || r >= m || c < 0 || c >= n || grid2[r][c] !== 1) return true;
        if (grid1[r][c] !== 1) return false;
        grid2[r][c] = 2;
        let isSub = true;
        for (let [dr, dc] of dir) {
            isSub &= isSubland(r + dr, c + dc);
        }
        return isSub;
    };

    let ans = 0;
    for (let r = 0; r < m; r++) {
        for (let c = 0; c < n; c++) {
            if (grid2[r][c] === 1) {
                ans += isSubland(r, c);
            }
        }
    }
    return ans;
};
```