# Transpose Matrix

Given a 2D integer array matrix, return the transpose of matrix.

## Approach 

``` C++
    vector<vector<int>> transpose(vector<vector<int>>& matrix) {
        int m = matrix.size();
        int n = matrix[0].size();

        std::vector<std::vector<int>> ans(n, std::vector<int>(m, 0));
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < m; j++)
            {
                ans[i][j] = matrix[j][i];
            }
        }
        return ans;
    }
```