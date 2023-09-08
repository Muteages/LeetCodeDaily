# Extra Characters in a String

https://leetcode.com/problems/extra-characters-in-a-string/description

You are given a 0-indexed string s and a dictionary of words dictionary. You have to break s into one or more non-overlapping substrings such that each substring is present in dictionary. There may be some extra characters in s which are not present in any of the substrings.

Return the minimum number of extra characters left over if you break up s optimally.


``` C++
    int minExtraChar(string s, vector<string>& dictionary) {
        int len = s.length();
        std::vector<int> dp(len + 1, INT_MAX);
        dp[len] = 0;

        for (int i = len - 1; i >= 0; i--)
        {
            for (std::string& str : dictionary)
            {
                int l = str.length();
                if (i + l <= len && s.substr(i, l) == str)
                {
                    dp[i] = std::min(dp[i], dp[i + l]);
                }
            }
           dp[i] = std::min(dp[i], dp[i + 1] + 1); 
        }

        return dp[0];
    }
```