# Pascal's Triangle

https://leetcode.com/problems/pascals-triangle/description

Given an integer numRows, return the first numRows of Pascal's triangle.


## Approach

``` C++
    vector<vector<int>> generate(int numRows) {
        std::vector<std::vector<int>> pascal(numRows);
        for (int i = 0; i < numRows; i++)
        {
            std::vector<int> curRow(i + 1, 1);
            if (i >= 2)
            {
                for (int j = 1; j < i; j++)
                {
                    curRow[j] = pascal[i - 1][j - 1] + pascal[i - 1][j];
                }
            }
            pascal[i] = curRow;
        }
        return pascal;
    }
```