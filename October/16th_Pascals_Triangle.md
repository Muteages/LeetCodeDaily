# Pascals Triangle

https://leetcode.com/problems/pascals-triangle-ii

Given an integer rowIndex, return the rowIndexth (0-indexed) row of the Pascal's triangle.

## Approach 

``` C++
    vector<int> getRow(int rowIndex) {
        std::vector<int> prev(1, 1);
        for (int i = 1; i <= rowIndex; i++)
        {
            std::vector<int> curr(i + 1, 1);
            for (int j = 1; j < i; j++)
            {
                curr[j] = prev[j - 1] + prev[j];
            }
            prev = curr;
        }
        return prev;
    }
```