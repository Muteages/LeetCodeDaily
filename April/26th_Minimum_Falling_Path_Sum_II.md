# Minimum Falling Path Sum II

https://leetcode.com/problems/minimum-falling-path-sum-ii/

Given an n x n integer matrix grid, return the minimum sum of a falling path with non-zero shifts.

A falling path with non-zero shifts is a choice of exactly one element from each row of grid such that no two elements chosen in adjacent rows are in the same column.

## Approach 1

``` C++
    int minFallingPathSum(vector<vector<int>>& grid) {
        int n = grid.size();
        std::vector<int> prev = grid[0];
        std::vector<int> curr(n, INT_MAX);
        for (int row = 1; row < n; row++)
        {
            for (int col = 0; col < n; col++)
            {
                int curCell = grid[row][col];
                for (int i = 0; i < n; i++)
                {
                    if (i == col)
                    {
                        continue;
                    }
                    if (curr[col] == prev[col])
                    { // yet calculate
                        curr[col] = prev[i] + curCell;
                    }
                    else
                    {
                        curr[col] = std::min(curr[col], prev[i] + curCell);
                    }
                }
            }
            prev = curr;
        }
        return *min_element(prev.begin(), prev.end());
    }
```

## Approach 2

Instead calculating all possible results, we could just find the first two smallest elements in previous row and add them to current row.

``` C++
    int minFallingPathSum(vector<vector<int>>& grid) {
        int n = grid.size();
        for (int row = 1; row < n; row++)
        {
            auto prev = grid[row - 1];
            nth_element(prev.begin(), prev.begin() + 1, prev.end());
            const int smallest = prev[0], secondSmallest = prev[1]; 
            for (int col = 0; col < n; col++)
            {
                if (smallest == grid[row - 1][col])
                { // If the current cell and the previous adjacent smallest cell in the same column, add the second smallest cell.
                    grid[row][col] += secondSmallest;
                }
                else
                {
                    grid[row][col] += smallest;
                }
            }
        }
        return *min_element(grid.back().begin(), grid.back().end());
    }
```