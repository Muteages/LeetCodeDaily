# Is Subsequence

https://leetcode.com/problems/is-subsequence

Given two strings s and t, return true if s is a subsequence of t, or false otherwise.

A subsequence of a string is a new string that is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (i.e., "ace" is a subsequence of "abcde" while "aec" is not).


## Approach 1

Traverse the string s

``` C++
    bool isSubsequence(string s, string t) {
        size_t sPos = 0;
        size_t tPos = 0;
        while (sPos < s.length())
        {
            if (t.find(s[sPos], tPos) != std::string::npos)
            {
                idx = t.find(s[sPos], tPos) + 1;
                sPos++;
            }
            else
            {
                return false;
            }
        }
        return true;
    }
```

## Approach 2

Traverse the string t

``` C++
    bool isSubsequence(string s, string t) {
        size_t sPos = 0;
        for (size_t tPos = 0; tPos < t.length(); tPos++)
        {
            if (s[sPos] == t[tPos])
            {
                sPos++;
            }

            if (sPos == s.length())
            {
                return true;
            }
        }
        return false;
    }
```