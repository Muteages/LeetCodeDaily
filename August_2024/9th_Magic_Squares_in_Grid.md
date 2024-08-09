# Magic Squares in Grid

https://leetcode.com/problems/magic-squares-in-grid

A 3 x 3 magic square is a 3 x 3 grid filled with distinct numbers from 1 to 9 such that each row, column, and both diagonals all have the same sum.

Given a row x col grid of integers, how many 3 x 3 contiguous magic square subgrids are there?

Note: while a magic square can only contain numbers from 1 to 9, grid may contain numbers up to 15.



## Approach

``` C++
    inline bool isMagic(vector<vector<int>>& grid, int centreRow, int centreCol)
    {
        if (grid[centreRow - 1][centreCol - 1] + grid[centreRow + 1][centreCol + 1] !=
            grid[centreRow - 1][centreCol + 1] + grid[centreRow + 1][centreCol - 1])
        { // Current subgrid has different diagonals sum
            return false;
        }

        std::bitset<10> unique;
        std::vector<int> rowSums(3, 0), colSums(3, 0);
        for (int row = centreRow - 1; row <= centreRow + 1; row++)
        {
            for (int col = centreCol - 1; col <= centreCol + 1; col++)
            {
                int val = grid[row][col];
                if (val > 9 || val < 1) return false;
                unique.flip(val);
                rowSums[row - centreRow + 1] += val;
                colSums[col - centreCol + 1] += val;
            }
        }

        if (unique.count() != 9) return false; // Doesn't inlcude 1~9

        const int rowSum = rowSums[0], colSum = colSums[0];
        for (int i = 1; i < 3; i++)
        {
            if (rowSums[i] != rowSum || colSums[i] != colSum)
            {
                return false;
            }
        }
        return true;
    }

    int numMagicSquaresInside(vector<vector<int>>& grid) {
        int m = grid.size(), n = grid[0].size();
        if (m < 3 || n < 3) return 0;
        int ans = 0;
        for (int centreRow = 1; centreRow <= m - 2; centreRow++)
        {
            for (int centreCol = 1; centreCol <= n - 2; centreCol++)
            {
                ans += isMagic(grid, centreRow, centreCol);
            }
        }
        return ans;
    }
```