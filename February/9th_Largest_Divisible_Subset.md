# Largest Divisible Subset

https://leetcode.com/problems/largest-divisible-subset

Given a set of distinct positive integers nums, return the largest subset answer such that every pair (answer[i], answer[j]) of elements in this subset satisfies:

answer[i] % answer[j] == 0, or
answer[j] % answer[i] == 0
If there are multiple solutions, return any of them.

## Approach 1

``` C++
    vector<int> largestDivisibleSubset(vector<int>& nums) {
        std::sort(nums.begin(), nums.end());
        int n = nums.size();
        std::vector<std::vector<int>> dp(n);
        int lds{}; // Record the lds index
        for (int i = 0; i < n; i++)
        {
            dp[i].emplace_back(nums[i]); // Insert itself first
            for (int j = i - 1; j >= 0; j--)
            {
                if (nums[i] % nums[j] == 0 && dp[i].size() < (dp[j].size() + 1))
                { // Possible divisible subset element
                    dp[i] = dp[j];
                    dp[i].emplace_back(nums[i]);
                }
            }
            lds = dp[i].size() > dp[lds].size() ? i : lds; // Update the lds index 
        }
        return dp[lds];
    }
```

## Approach 2

Optimal Solution

``` C++
    vector<int> largestDivisibleSubset(vector<int>& nums) {
        std::sort(nums.begin(), nums.end());
        int n = nums.size();
        std::vector<int> dp(n, 1); // Record the largest subset size at each number.
        std::vector<int> link(n, -1); // Record the largest subset elements' indices
        int last = 0; // Record the last element's index at lds
        for (int i = 1; i < n; i++)
        {
            for (int j = 0; j < i; j++)
            {
                if (nums[i] % nums[j] == 0 && dp[i] < dp[j] + 1)
                { // Find a new possible lds
                    dp[i] = dp[j] + 1;
                    link[i] = j;
                }
            }
            // Update the new lds's last index
            last = dp[i] > dp[last] ? i : last;
        }

        std::vector<int> ans;
        while (last != -1)
        {
            ans.emplace_back(nums[last]);
            last = link[last];
        }
        return ans;
    }
```


