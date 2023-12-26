# Number of Dice Rolls with Target Sum

https://leetcode.com/problems/number-of-dice-rolls-with-target-sum

You have n dice, and each die has k faces numbered from 1 to k.

Given three integers n, k, and target, return the number of possible ways (out of the kn total ways) to roll the dice, so the sum of the face-up numbers equals target. Since the answer may be too large, return it modulo 109 + 7.

## Approach 1

``` C++
    const int mod = 1e9 + 7;
    std::vector<std::vector<int>> dp;

    int calculateDice(int n, int k, int target)
    {
        if (n== 0 && target == 0)
        { // Reach the end
            return 1;
        }
        if (n == 0 || target <= 0)
        { // Failed to get the target
            return 0;
        }

        if (dp[n][target] != -1)
        { // Reuse the result
            return dp[n][target] % mod;
        }

        int curWays = 0;
        for (int i = 1; i <= k; i++)
        {
            curWays = (curWays + calculateDice(n - 1, k, target - i)) % mod;
        }
        dp[n][target] = curWays;
        return dp[n][target];
    }
public:
    int numRollsToTarget(int n, int k, int target) {
        dp.resize(n + 1, std::vector<int>(target + 1, -1));
        return calculateDice(n, k, target);
    }
```

## Approach 2

``` C++
    int numRollsToTarget(int n, int k, int target) {
        const int mod = 1e9 + 7;
        std::vector<std::vector<int>> dp(n + 1, std::vector<int>(target + 1, 0));
        dp[0][0] = 1;
        for (int dice = 1; dice <= n; dice++)
        {
            for (int sum = 1; sum <= target; sum++)
            {
                for (int face = 1; face <= std::min(k, sum); face++)
                {
                    dp[dice][sum] = (dp[dice][sum] + dp[dice - 1][sum - face]) % mod;
                }
            }
        }
        return dp[n][target];
    }
```