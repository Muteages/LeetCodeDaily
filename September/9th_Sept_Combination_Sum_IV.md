# Combination Sum IV

https://leetcode.com/problems/combination-sum-iv/description/

Given an array of distinct integers nums and a target integer target, return the number of possible combinations that add up to target.

## Approach

``` C++
    int combinationSum4(vector<int>& nums, int target) {
        std::sort(nums.begin(), nums.end());

        if (nums[0] > target)
        { // Unable to combine nums to target since the smallest number is greater than the target
            return 0;
        }

        std::vector<size_t> dp(target + 1, 0);
        dp[0] = 1;

        for (int i = 1; i <= target; i++)
        {
            for (const auto& num : nums)
            {
                if (i - num >= 0)
                {
                    dp[i] += dp[i - num];
                }
                else
                { // Remaining numbers are all greater than the target number
                    break;
                }
            }
        }

        return dp[target];
    }
```
