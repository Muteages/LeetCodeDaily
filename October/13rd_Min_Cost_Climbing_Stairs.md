# Min Cost Climbing Stairs

https://leetcode.com/problems/min-cost-climbing-stairs

You are given an integer array cost where cost[i] is the cost of ith step on a staircase. Once you pay the cost, you can either climb one or two steps.

You can either start from the step with index 0, or the step with index 1.

Return the minimum cost to reach the top of the floor.

## Approach 

``` C++
    int minCostClimbingStairs(vector<int>& cost) {
        int n = cost.size();
        std::vector<int> dp(n, 0);
        dp[0] = cost[0];
        dp[1] = cost[1];
        for (int i = 2; i < n; i++)
        {
            dp[i] = cost[i] + std::min(dp[i - 1], dp[i - 2]);
        }
        return std::min(dp[n - 1], dp[n - 2]);
    }
```