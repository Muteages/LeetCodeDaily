# Find Longest Special Substring that Occurs Thrice

https://leetcode.com/problems/find-longest-special-substring-that-occurs-thrice-i

You are given a string s that consists of lowercase English letters.

A string is called special if it is made up of only a single character. For example, the string "abc" is not special, whereas the strings "ddd", "zz", and "f" are special.

Return the length of the longest special substring of s which occurs at least thrice, or -1 if no special substring occurs at least thrice.

A substring is a contiguous non-empty sequence of characters within a string.


## Approach 1 

Brute force
``` C++
    int maximumLength(string s) {
        int len = s.length();
        std::unordered_map<std::string, int> freq;
        int ans = -1;
        for (int l = 0; l < len; l++)
        {
            std::string curr(1, s[l]);
            for (int r = l + 1; r <= len; r++)
            {
                freq[curr]++;
                if (freq[curr] == 3)
                {
                    ans = std::max(ans, static_cast<int>(curr.length()));
                }
                if (r == len || s[r] != curr.back())
                { // Not special, count the substring and break
                    break;
                }
                // Special, add it to current substring
                curr += s[r];
            }
        }
        return ans;       
    }
```

Avoid hash map and string cpoy to get better performance.
``` C++
    int maximumLength(string s) {
        int n = s.size(), prev = s[0];
        std::vector<std::vector<int>> freq(26, std::vector<int>(n + 1, 0)); // freq[i][j] represents the j length of i's frequency
        int curLen = 0;
        for (int i = 0; i < n; i++)
        {
            if (s[i] == prev) 
            {
                curLen++;
            }
            else
            {
                curLen = 1;
                prev = s[i];
            }
            freq[s[i] - 'a'][curLen]++;
        }

        int ans = -1;
        for (int i = 0; i < 26; i++)
        {
            int len = 0;
            for (int j = n; j > 0; j--)
            {
                len += freq[i][j];
                if (len >= 3)
                {
                    ans = std::max(ans, j);
                    break;
                }
            }
        }
        return ans;
    }
```