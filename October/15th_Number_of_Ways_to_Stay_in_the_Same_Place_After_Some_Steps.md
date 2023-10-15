# Number of Ways to Stay in the Same Place After Some Steps

https://leetcode.com/problems/number-of-ways-to-stay-in-the-same-place-after-some-steps

You have a pointer at index 0 in an array of size arrLen. At each step, you can move 1 position to the left, 1 position to the right in the array, or stay in the same place (The pointer should not be placed outside the array at any time).

Given two integers steps and arrLen, return the number of ways such that your pointer is still at index 0 after exactly steps steps. Since the answer may be too large, return it modulo 109 + 7.

## Approach 1
2D DP

``` C++
    int numWays(int steps, int arrLen) {
        const int mod = 1e9 + 7;
        int maxLen = steps / 2 + 1; // If we reach a position beyond this len, we can't go back to 0 position
        int len = std::min(maxLen, arrLen);

        std::vector<std::vector<int>> dp(steps + 1, std::vector<int>(len, 0));
        dp[0][0] = 1;
        for (int i = 1; i <= steps; i++)
        {
            for (int j = 0; j < len; j++)
            {
                dp[i][j] = dp[i - 1][j]; // Stay 
                if (j > 0)
                { // Move left
                    dp[i][j] = (dp[i][j] + dp[i - 1][j - 1]) % mod;
                }
                if (j < len - 1)
                { // Move right
                    dp[i][j] = (dp[i][j] + dp[i - 1][j + 1]) % mod;
                }
            }
        }
        return dp[steps][0];
    }
```

## Approach 2

1D DP

``` C++ 
    int numWays(int steps, int arrLen) {
        const int mod = 1e9 + 7;
        int maxLen = steps / 2 + 1; // If we reach a position beyond this len, we can't go back to 0 position
        int len = std::min(maxLen, arrLen);

        std::vector<int> prev(len + 1, 0);
        std::vector<int> curr(len + 1, 0);
        prev[0] = 1;
        for (int i = 1; i <= steps; i++)
        {
            for (int j = 0; j <= len; j++)
            {
                curr[j] = prev[j]; // Stay
                if (j > 0)
                { // Move left
                    curr[j] = (curr[j] + prev[j - 1]) % mod;
                }
                if (j < len - 1)
                { // Move right
                    curr[j] = (curr[j] + prev[j + 1]) % mod;
                }                
            }
            std::swap(curr, prev);
        }
        return prev[0];
    }
```