# Element Appearing More Than 25% In Sorted Array

https://leetcode.com/problems/element-appearing-more-than-25-in-sorted-array

Given an integer array sorted in non-decreasing order, there is exactly one integer in the array that occurs more than 25% of the time, return that integer.

## Approach 

``` C++
    int findSpecialInteger(vector<int>& arr) {
        int n = arr.size();
        if (n == 1)
        {
            return arr.back();
        }
        int threshold = n / 4;
        for (int i = 0; i < n - threshold; i++)
        {
            if (arr[i] == arr[i + threshold])
            {
                return arr[i];
            }
        }
        return -1;
    }
```