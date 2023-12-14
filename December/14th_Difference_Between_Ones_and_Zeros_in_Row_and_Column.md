# Difference Between Ones and Zeros in Row and Column

https://leetcode.com/problems/difference-between-ones-and-zeros-in-row-and-column

You are given a 0-indexed m x n binary matrix grid.

A 0-indexed m x n difference matrix diff is created with the following procedure:

Let the number of ones in the ith row be onesRowi.
Let the number of ones in the jth column be onesColj.
Let the number of zeros in the ith row be zerosRowi.
Let the number of zeros in the jth column be zerosColj.
diff[i][j] = onesRowi + onesColj - zerosRowi - zerosColj
Return the difference matrix diff.

## Approach 

``` C++
    vector<vector<int>> onesMinusZeros(vector<vector<int>>& grid) {
        int m = grid.size();
        int n = grid[0].size();

        std::vector<int> onesRow(m, 0);    // Store the number of 1 in each row
        std::vector<int> onesColumn(n, 0); // Store the number of 1 in each column

        for (int i = 0; i < m; i++)
        {
            for (int j = 0; j < n; j++)
            {
                if (grid[i][j] == 1)
                {
                    onesRow[i]++;
                    onesColumn[j]++;
                }
            }
        }
        std::vector<std::vector<int>> diff(m, std::vector<int>(n, 0));
        for (int i = 0; i < m; i++)
        {
            for (int j = 0; j < n; j++)
            {
                // the number of 0 = total - the number of 1
                int zeroRow = n - onesRow[i];
                int zeroColumn = m - onesColumn[j];

                diff[i][j] = onesRow[i] + onesColumn[j] - zeroRow - zeroColumn;
            }
        }
        return diff;
    }
```