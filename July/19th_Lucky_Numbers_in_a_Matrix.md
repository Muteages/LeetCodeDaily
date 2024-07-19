# Lucky Numbers in a Matrix

https://leetcode.com/problems/lucky-numbers-in-a-matrix

Given an m x n matrix of distinct numbers, return all lucky numbers in the matrix in any order.

A lucky number is an element of the matrix such that it is the minimum element in its row and maximum in its column.


## Approach 

``` C++
    vector<int> luckyNumbers (vector<vector<int>>& matrix) {
        int m = matrix.size(), n = matrix[0].size();
        std::vector<int> minRows(m, -1);
        for (int row = 0; row < m; row++)
        {
            int minCol = std::min_element(matrix[row].begin(), matrix[row].end()) - matrix[row].begin();
            minRows[row] = minCol;
        }
        std::vector<int> ans;
        for (int i = 0; i < m; i++)
        {
            int col = minRows[i], number = matrix[i][col];
            bool isMax = true;
            for (int row = 0; row < m; row++)
            {
                if (matrix[row][col] > number)
                {
                    isMax = false;
                    break;
                }
            }
            if (isMax)
            {
                ans.emplace_back(number);
            }
        }
        return ans;
    }
```

``` C++
    bool isMaxOfCol(const std::vector<std::vector<int>>& mat, int maxOfCol, int col)
    {
        for (int row = 0; row < mat.size(); row++)
        {
            if (mat[row][col] > maxOfCol)
            {
                return false;
            }
        }
        return true;
    }
    vector<int> luckyNumbers (vector<vector<int>>& matrix) {
        int m = matrix.size(), n = matrix[0].size();
        for (int row = 0; row < m; row++)
        {
            int minCol = std::min_element(matrix[row].begin(), matrix[row].end()) - matrix[row].begin();
            int minOfRow = matrix[row][minCol];
            if (isMaxOfCol(matrix, minOfRow, minCol))
            {
                return {minOfRow};
            }
        }
        return {};
    }
```



``` JavaScript
var luckyNumbers  = function(matrix) {
    for (let row of matrix) {
        let minOfRow = Math.min(...row);
        let col = row.indexOf(minOfRow);
        if (matrix.every(ele => ele[col] <= minOfRow)) {
            return [minOfRow];
        }
    }
    return [];
};
```

