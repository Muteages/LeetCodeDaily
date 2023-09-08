# Interleaving String

https://leetcode.com/problems/interleaving-string/description/

Given strings s1, s2, and s3, find whether s3 is formed by an interleaving of s1 and s2.


## Approach 

Use 2D-DP. Create a 2D vector to track the concatenation process.

``` C++
    bool isInterleave(string s1, string s2, string s3) {
        int l1 = s1.length();
        int l2 = s2.length();
        int l3 = s3.length();

        if (l1 + l2 != l3)
        {
            return false;
        }

        // 2D - DP 
        std::vector<std::vector<bool>> dp(l1 + 1, std::vector<bool>(l2 + 1, false));
        dp[0][0] = true;

        // Set s1, s2 respectively first. i.e the first row and column

        for (int i = 1; i <= l1; i++)
        {
            dp[i][0] = dp[i - 1][0] && s1[i - 1] == s3[i - 1];
        }

        for (int j = 1; j <= l2; j++)
        {
            dp[0][j] = dp[0][j - 1] && s2[j - 1] == s3[j - 1];
        }

        // Now go through the 2D vector.  Only go down or right
        for (int i = 1; i <= l1; i++)
        {
            for (int j = 1; j <= l2; j++)
            {
                dp[i][j] = (dp[i - 1][j] && s1[i - 1] == s3[i + j - 1]) ||
                    (dp[i][j - 1] && s2[j - 1] == s3[i + j - 1]);
            }
        }
        
        return dp[l1][l2];
    }
```