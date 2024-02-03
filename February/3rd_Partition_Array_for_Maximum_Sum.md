# Partition Array for Maximum Sum

https://leetcode.com/problems/partition-array-for-maximum-sum

Given an integer array arr, partition the array into (contiguous) subarrays of length at most k. After partitioning, each subarray has their values changed to become the maximum value of that subarray.

Return the largest sum of the given array after partitioning. Test cases are generated so that the answer fits in a 32-bit integer.

## Approach 

``` C++
    int maxSumAfterPartitioning(vector<int>& arr, int k) {
        int n = arr.size();

        std::vector<int> dp(n + 1, 0);
        for (int i = 1; i <= n; i++)
        {
            int curMax{}, curSum{};
            for (int j = 1; j <= std::min(i, k); j++)
            {
                curMax = std::max(curMax, arr[i - j]);
                curSum = std::max(curSum, dp[i - j] + curMax * j);
            }
            dp[i] = curSum;
        }
        return dp.back();
    }
```

