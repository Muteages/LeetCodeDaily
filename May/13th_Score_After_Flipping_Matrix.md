# Score After Flipping Matrix

https://leetcode.com/problems/score-after-flipping-matrix

A move consists of choosing any row or column and toggling each value in that row or column (i.e., changing all 0's to 1's, and all 1's to 0's).

Every row of the matrix is interpreted as a binary number, and the score of the matrix is the sum of these numbers.

Return the highest possible score after making any number of moves (including zero moves).


## Approach 

``` C++
    int matrixScore(vector<vector<int>>& grid) {
        int m = grid.size(), n = grid[0].size();
        // Assume all grid[row][0] == 1, which represent the value 1 << (n - 1)
        int ans = m * (1 << (n - 1));

        for (int col = 1; col < n; col++)
        {
            int numOfOne = 0;
            for (int row = 0; row < m; row++)
            {
                numOfOne += grid[row][col] == grid[row][0]; // Since we need to flip grid[row][0] to 1, cells which have the same bit with grid[row][0] will be 1 eventually
            }
            ans += std::max(numOfOne, m - numOfOne) * (1 << (n - 1 - col));
        }
        return ans;
    }
```