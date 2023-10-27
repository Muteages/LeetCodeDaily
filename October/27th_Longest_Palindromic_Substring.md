# Longest Palindromic Substring

https://leetcode.com/problems/longest-palindromic-substring

Given a string s, return the longest palindromic substring in s.

## Approach 1

Brute force

``` C++
    bool isPlindrome(const std::string& str, int i, int j)
    {
        while (i <= j)
        {
            if (str[i] != str[j])
            {
                return false;
            }
            i++;
            j--;
        }
        return true;
    }
    string longestPalindrome(string s) {
        int st = 0;
        int maxLength = -1;
        for (int i = 0; i < s.length(); i++)
        {
            for (int j = i; j < s.length(); j++)
            {
                if (j - i < maxLength)
                { // Shorter than previous length
                    continue;
                }
                if (isPlindrome(s, i, j) && (j - i + 1 > maxLength))
                {
                    maxLength = j - i + 1;
                    st = i;
                }
            } 
        }
        return s.substr(st, maxLength);
    }
```

## Approach 2

``` C++
    std::string ans = "";
    void expandString(const std::string& s, int left, int right)
    {
        while (left >= 0 && right < s.length())
        {
            if (s[left] != s[right])
            {
                break;
            }
            left--;
            right++;
        }

        // current palindrome [left + 1, right - 1]
        int curLen = right - 1 - (left + 1) + 1; 
        if (curLen > ans.length())
        {
            ans = s.substr(left + 1, curLen);
        }
    }
    string longestPalindrome(string s) {
        for (size_t i = 0; i < s.length(); i++)
        {
            expandString(s, i, i); // odd 
            expandString(s, i, i + 1); // even
        }
        return ans;
    }
```
