# Sum of Absolute Differences in a Sorted Array

https://leetcode.com/problems/sum-of-absolute-differences-in-a-sorted-array

You are given an integer array nums sorted in non-decreasing order.

Build and return an integer array result with the same length as nums such that result[i] is equal to the summation of absolute differences between nums[i] and all the other elements in the array.

In other words, result[i] is equal to sum(|nums[i]-nums[j]|) where 0 <= j < nums.length and j != i (0-indexed).

## Approach 1

Brute force. TLE for large cases

``` C++
    vector<int> getSumAbsoluteDifferences(vector<int>& nums) {
        int n = nums.size();
        std::vector<int> ans(n, 0);
        for (int i = 0; i < n; i++)
        {
            int sum = 0;
            for (int j = 0; j < n; j++)
            {
                sum += std::abs(nums[i] - nums[j]);
            }
            ans[i] = sum;
        }
        return ans;
    }
```

## Approach 2

Prefix and suffix
``` C++
    vector<int> getSumAbsoluteDifferences(vector<int>& nums) {
        int n = nums.size();
        std::vector<int> prefix(nums);
        std::vector<int> suffix(nums);

        for (int i = 1, j = n - 2; i < n; i++, j--)
        {
            prefix[i] += prefix[i - 1];
            suffix[j] += suffix[j + 1];
        }

        std::vector<int> ans(n, 0);
        for (int i = 0; i < n; i++)
        {
            ans[i] = ((i + 1) * nums[i] - prefix[i]) + (suffix[i] - (n - i) * nums[i]);
        }
        return ans;
    }
```

## Approach 3

``` C++
    vector<int> getSumAbsoluteDifferences(vector<int>& nums) {
        int sum = std::accumulate(nums.begin(), nums.end(), 0);
        int prefix = 0;
        int suffix = sum;

        int n = nums.size();
        std::vector<int> ans(n, 0);
        for (int i = 0; i < n; i++)
        {
            suffix -= nums[i];
            ans[i] = (nums[i] * i - prefix) + (suffix - nums[i] * (n - i - 1));
            prefix += nums[i];
        }
        return ans;
    }
```