# Longest Ideal Subsequence

https://leetcode.com/problems/longest-ideal-subsequence

You are given a string s consisting of lowercase letters and an integer k. We call a string t ideal if the following conditions are satisfied:

t is a subsequence of the string s.
The absolute difference in the alphabet order of every two adjacent letters in t is less than or equal to k.
Return the length of the longest ideal string.

A subsequence is a string that can be derived from another string by deleting some or no characters without changing the order of the remaining characters.

## Approach 

``` C++
    int longestIdealString(string s, int k) {
        int len = s.length();
        if (k == 25)
        {
            return len;
        }
        int ans = 1;
        std::vector<int> dp(26, 0);
        for (const char ch : s)
        {
            int i = ch - 'a';
            int left = std::max(0, i - k);
            int right = std::min(i + k, 25);
            for (int j = left; j <= right; j++)
            {
                dp[i] = std::max(dp[i], dp[j]);
            }
            dp[i]++; // Add itself
            ans = std::max(ans, dp[i]);
        }
        return ans;
    }
```

