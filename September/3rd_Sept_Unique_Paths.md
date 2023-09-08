# Unique Paths

https://leetcode.com/problems/unique-paths/description

There is a robot on an m x n grid. The robot is initially located at the top-left corner (i.e., grid[0][0]). The robot tries to move to the bottom-right corner (i.e., grid[m - 1][n - 1]). The robot can only move either down or right at any point in time.

Given the two integers m and n, return the number of possible unique paths that the robot can take to reach the bottom-right corner.


## Approach 1
``` C++
    int uniquePaths(int m, int n) {
        int ans = 0;
        std::vector<std::vector<int>> dp(m, std::vector<int>(n, 0));  // Store the possible ways to each cell

        // Initialise
        for (int i = 0; i < n; i++)
        {
            dp[0][i] = 1;
        }

        for (int i = 0; i < m; i++)
        {
            dp[i][0] = 1;
        }

        
        for (int i = 1; i < m; i++)
        {
            for (int j = 1; j < n; j++)
            {   // The current cell can only be reached by left or up cells.
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
            }
        }
        return dp[m-1][n-1];
    }
```

## Approach 2 

Since we only need the previous row and current row, we can use only 1D vector to store info

``` C++
    int uniquePaths(int m, int n) {
        std::vector<int> prevRow(n, 1);  // Record the previous row line

        for (int i = 1; i < m; i++)
        {
            std::vector<int> curRow(n, 1); // Current row
            for (int j = 1; j < n; j++)
            {
                curRow[j] = curRow[j - 1] + prevRow[j];
            }
            prevRow = curRow; // Update the previous row
        }

        return prevRow.back();
    }
```
