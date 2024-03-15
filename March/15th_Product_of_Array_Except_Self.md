# Product of Array Except Self

https://leetcode.com/problems/product-of-array-except-self

Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].

The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.

You must write an algorithm that runs in O(n) time and without using division.


## Approach 1

``` C++
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        std::vector<int> ans(n);
        std::vector<int> prefix(n, 1), suffix(n, 1);
        for (int i = 1; i < n; i++)
        {
            prefix[i] = prefix[i - 1] * nums[i - 1];
            suffix[n - i - 1] = suffix[n - i] * nums[n - i];
        }

        for (int i = 0; i < n; i++)
        {
            ans[i] = prefix[i] * suffix[i];
        }
        return ans;
    }
```

## Approach 2

``` C++
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        std::vector<int> ans(n, 1);
        int prefix = 1, suffix = 1;
        for (int i = 0; i < n; i++)
        {
            ans[i] *= prefix;
            prefix *= nums[i];
            ans[n - i - 1] *= suffix;
            suffix *= nums[n - i - 1];
        }
        return ans;
    }
```
