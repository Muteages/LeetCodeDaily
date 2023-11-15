# Maximum Element After Decreasing and Rearranging

https://leetcode.com/problems/maximum-element-after-decreasing-and-rearranging

You are given an array of positive integers arr. Perform some operations (possibly none) on arr so that it satisfies these conditions:

The value of the first element in arr must be 1.
The absolute difference between any 2 adjacent elements must be less than or equal to 1.
There are 2 types of operations that you can perform any number of times:

Decrease the value of any element of arr to a smaller positive integer.
Rearrange the elements of arr to be in any order.
Return the maximum possible value of an element in arr after performing the operations to satisfy the conditions.

## Approach 

``` C++
    int maximumElementAfterDecrementingAndRearranging(vector<int>& arr) {
        std::sort(arr.begin(), arr.end());
        int ans = 1; // First element must be 1
        for (int i = 1; i < arr.size(); i++)
        {
            if (arr[i] - arr[i - 1] > 1)
            { // Need to decrease the number
                arr[i] = arr[i - 1] + 1;
            }
        }
        return arr.back();
    }
```