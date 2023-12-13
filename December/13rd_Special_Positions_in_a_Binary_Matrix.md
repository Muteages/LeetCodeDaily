# Special Positions in a Binary Matrix

https://leetcode.com/problems/special-positions-in-a-binary-matrix

Given an m x n binary matrix mat, return the number of special positions in mat.

A position (i, j) is called special if mat[i][j] == 1 and all other elements in row i and column j are 0 (rows and columns are 0-indexed).

## Approach 1

``` C++
    bool isSpecial(std::vector<std::vector<int>>& mat, int row, int col)
    {
        for (int i = 0; i < mat.size(); i++)
        { // Check current column
            if (i != row && mat[i][col] == 1)
            {
                return false;
            }
        }

        for (int j = 0; j < mat[0].size(); j++)
        { // Check current row
            if (j != col && mat[row][j] == 1)
            {
                return false;
            }
        }
        return true;
    }

    int numSpecial(vector<vector<int>>& mat) {
        int m = mat.size();
        int n = mat[0].size();
        int ans{};
        for (int row = 0; row < m; row++)
        {
            for (int col = 0; col < n; col++)
            {
                if (mat[row][col] == 1)
                {
                    ans += isSpecial(mat, row, col);
                }
            }
        }
        return ans;        
    }
```

## Approach 2

Additional set to track visited row and column
``` C++
    bool isSpecial(std::vector<std::vector<int>>& mat, int row, int col)
    {
        for (int i = 0; i < mat.size(); i++)
        { // Check current column
            if (i != row && mat[i][col] == 1)
            {
                return false;
            }
        }

        for (int j = 0; j < mat[0].size(); j++)
        { // Check current row
            if (j != col && mat[row][j] == 1)
            {
                return false;
            }
        }
        return true;
    }

    int numSpecial(vector<vector<int>>& mat) {
        int m = mat.size();
        int n = mat[0].size();
        int ans{};
        std::unordered_set<int> visitedRow;
        std::unordered_set<int> visitedCol;
        for (int row = 0; row < m; row++)
        {
            for (int col = 0; col < n; col++)
            {
                if (mat[row][col] == 1)
                {
                    if (visitedRow.count(row) || visitedCol.count(col))
                    { // Already exist
                        continue;
                    }
                    visitedRow.insert(row);
                    visitedCol.insert(col);
                    ans += isSpecial(mat, row, col);
                }
            }
        }
        return ans;        
    }
```

## Approach 3

``` C++
    int numSpecial(vector<vector<int>>& mat) {
        int m = mat.size();
        int n = mat[0].size();

        std::vector<int> rowSum(m, 0);
        std::vector<int> colSum(n, 0);
        for (int i = 0; i < m; i++)
        {
            for (int j = 0; j < n; j++)
            {
                if (mat[i][j] == 1)
                {
                    rowSum[i]++;
                    colSum[j]++;
                }
            }
        }

        int ans{};
        for (int i = 0; i < m; i++)
        {
            for (int j = 0; j < n; j++)
            {
                if (mat[i][j] == 1 && rowSum[i] == 1 && colSum[j] == 1)
                {
                    ans++;
                }
            }
        }
        return ans;
    }
```