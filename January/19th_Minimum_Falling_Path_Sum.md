# Minimum Falling Path Sum

https://leetcode.com/problems/minimum-falling-path-sum

Given an n x n array of integers matrix, return the minimum sum of any falling path through matrix.

A falling path starts at any element in the first row and chooses the element in the next row that is either directly below or diagonally left/right. Specifically, the next element from position (row, col) will be (row + 1, col - 1), (row + 1, col), or (row + 1, col + 1).


## Approach 

``` C++
    int minFallingPathSum(vector<vector<int>>& matrix) {
        int n = matrix.size();
        if (n == 1)
        {
            return matrix[0][0];
        }

        for (int i = n - 2; i >= 0; i--)
        {
            // The first and last cells only have two options. 
            matrix[i][0] += std::min(matrix[i + 1][0], matrix[i + 1][1]);
            matrix[i][n - 1] += std::min(matrix[i + 1][n - 1], matrix[i + 1][n - 2]);

            for (int j = 1; j < n - 1; j++)
            {
                matrix[i][j] += std::min({matrix[i + 1][j - 1], matrix[i + 1][j], matrix[i + 1][j + 1]});
            }
        }
        int ans = *std::min_element(matrix[0].begin(), matrix[0].end());
        return ans;
    }
```