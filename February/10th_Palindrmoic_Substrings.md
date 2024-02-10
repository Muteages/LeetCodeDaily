# Palindromic Substrings

https://leetcode.com/problems/palindromic-substrings

Given a string s, return the number of palindromic substrings in it.

A string is a palindrome when it reads the same backward as forward.

A substring is a contiguous sequence of characters within the string.

## Approach 1

Brute froce 

``` C++
    int countSubstrings(string s) {
        int len = s.length();
        int ans = len;
        for (int i = 0; i < len; i++)
        {
            std::string curr{};
            curr += s[i];
            for (int j = i + 1; j < len; j++)
            {
                curr += s[j];
                std::string temp(curr);
                std::reverse(temp.begin(), temp.end());
                if (curr == temp)
                {
                    ans++;
                }
            }
        }
        return ans;
    }
```

## Approach 2

expand the string from the current centre

``` C++
    int expandString(const string& s, int left, int right)
    {
        int cnt = 0;
        while (left >= 0 && right < s.length() && s[left] == s[right])
        {
            cnt++;
            left--;
            right++;
        }
        return cnt;
    }

    int countSubstrings(string s) {
        int len = s.length();
        int ans = 0;
        for (int i = 0; i < len; i++)
        {
            ans += expandString(s, i, i);
            ans += expandString(s, i, i + 1);
        }
        return ans;
    }
```
