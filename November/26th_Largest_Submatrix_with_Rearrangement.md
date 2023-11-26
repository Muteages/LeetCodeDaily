# Largest Submatrix with Rearrangement

https://leetcode.com/problems/largest-submatrix-with-rearrangements

You are given a binary matrix matrix of size m x n, and you are allowed to rearrange the columns of the matrix in any order.

Return the area of the largest submatrix within matrix where every element of the submatrix is 1 after reordering the columns optimally.

## Approach

``` C++
    int largestSubmatrix(vector<vector<int>>& matrix) {
        int m = matrix.size();
        int n = matrix[0].size();

        for (int i = 1; i < m; i++)
        {
            for (int j = 0; j < n; j++)
            {
                if (matrix[i][j] == 1)
                { // Calculate the height at current cell
                    matrix[i][j] += matrix[i - 1][j];
                }
            }
        }

        int ans = 0;
        for (int i = 0; i < m; i++)
        {
            std::sort(matrix[i].begin(), matrix[i].end());
            for (int j = 0; j < n; j++)
            { // Build the matrix
                int h = matrix[i][j];
                int w = n - j;
                ans = std::max(ans, h * w);
            }
        }
        return ans;
    }
```