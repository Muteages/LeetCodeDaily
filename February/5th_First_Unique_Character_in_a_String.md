# First Unique Character in a String

https://leetcode.com/problems/first-unique-character-in-a-string

Given a string s, find the first non-repeating character in it and return its index. If it does not exist, return -1.

## Approach 

``` C++
    int firstUniqChar(string s) {
        std::vector<int> occurrences(26, 0);
        for (const auto& ch : s)
        {
            occurrences[ch - 'a']++;
        }

        for (int i = 0; i < s.length(); i++)
        {
            if (occurrences[s[i] - 'a'] == 1)
            {
                return i;
            }
        }
        return -1;
    }
```

