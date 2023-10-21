# Constrained Subsequence Sum

https://leetcode.com/problems/constrained-subsequence-sum

Given an integer array nums and an integer k, return the maximum sum of a non-empty subsequence of that array such that for every two consecutive integers in the subsequence, nums[i] and nums[j], where i < j, the condition j - i <= k is satisfied.

A subsequence of an array is obtained by deleting some number of elements (can be zero) from the array, leaving the remaining elements in their original order.


## Approach 1

TLE for big cases
``` C++
    int constrainedSubsetSum(vector<int>& nums, int k) {
        std::vector<int> dp(nums.size());
        for (int j = 0; j < dp.size(); j++)
        {
            int prevMax = 0;
            for (int i = j - k; i < j; i++)
            {
                if (i >= 0)
                {
                    prevMax = std::max(prevMax, dp[i]);
                }
            }
            dp[j] = nums[j] + prevMax;
        }
        int ans = *std::max_element(dp.begin(), dp.end());
        return ans;
    }
```

## Approach 2

``` C++
    int constrainedSubsetSum(vector<int>& nums, int k) {
        std::priority_queue<std::pair<int, int>> pq; // Current max sum - idx
        pq.emplace(nums[0], 0);
        int ans = nums[0];
        for (int i = 1; i < nums.size(); i++)
        {
            while (pq.top().second < i - k)
            { // Out of range, remove the record
                pq.pop();
            }

            int currMax = std::max(0, pq.top().first) + nums[i];
            ans = std::max(ans, currMax);
            pq.emplace(currMax, i);
        }

        return ans;
    }
```

## Approach 3

``` C++
    int constrainedSubsetSum(vector<int>& nums, int k) {
        std::map<int, int> mp; // max sum - frequency
        mp[0] = 0;
        std::vector<int> dp(nums.size());

        for (int i = 0; i < nums.size(); i++)
        {
            dp[i] = nums[i] + mp.rbegin()->first;
            mp[dp[i]]++;

            if (i >= k)
            { // Out of range 
                int outSum = dp[i - k];
                mp[outSum]--;
                if (mp[outSum] == 0)
                {
                    mp.erase(outSum);
                }
            }
        }
        int ans = *std::max_element(dp.begin(), dp.end());
        return ans;
    }
```