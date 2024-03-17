# Contiguous Array

https://leetcode.com/problems/contiguous-array/

Given a binary array, find the maximum length of a contiguous subarray with equal number of 0 and 1.

## Approach

``` C++
    int findMaxLength(vector<int>& nums) {
        int n = nums.size();
        int sum = 0;
        int ans = 0;
        std::unordered_map<int, int> prefix; // prefix sum - index
        for (int i = 0; i < n; i++)
        {
            sum += nums[i] == 1 ? 1 : -1;
            if (sum == 0)
            { // If the sum is 0, then the current subarray is the longest subarray with equal number of 0 and 1.
                ans = i + 1;
            }
            else if (prefix.count(sum))
            {
                ans = std::max(ans, i - prefix[sum]);
            }
            else
            {
                prefix[sum] = i;
            }
        }
        return ans;
    }
```
