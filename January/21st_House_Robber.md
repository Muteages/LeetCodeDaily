# House Robber

https://leetcode.com/problems/house-robber

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given an integer array nums representing the amount of money of each house, return the maximum amount of money you can rob tonight without alerting the police.

## Approach 1

Maintain a dp vector to record the maximum money at each house

``` C++
    int rob(vector<int>& nums) {
        int n = nums.size();
        if (n == 1)
        {
            return nums[0];
        }
        else if (n == 2)
        {
            return std::max(nums[0], nums[1]);
        }
        std::vector<int> dp(n, 0);
        dp[0] = nums[0];
        dp[1] = std::max(nums[0], nums[1]);
        for (int i = 2; i < n; i++)
        { // Two options: rob the current house or skip the current house
            dp[i] = std::max(dp[i - 2] + nums[i], dp[i - 1]);
        }
        return dp[n - 1];
    }
```

## Approach 2

Replace the vector with two variables

``` C++
    int rob(vector<int>& nums) {
        int prev = 0, curr = 0;
        for (int i = 0; i < nums.size(); i++)
        {
            int temp = std::max(prev + nums[i], curr);
            prev = curr;
            curr = temp;
        }
        return curr;
    }
```

