# Valid Anagram

https://leetcode.com/problems/valid-anagram

Given two strings s and t, return true if t is an anagram of s, and false otherwise.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

## Approach

Or use unordered_map to build frequency map
``` C++
    bool isAnagram(string s, string t) {
        if (s.size() != t.size())
        {
            return false;
        }

        std::vector<int> counts(26, 0);
        for (int i = 0; i < s.size(); i++)
        {
            counts[s[i] - 'a']++;
            counts[t[i] - 'a']--;
        }

        for (int count : counts)
        {
            if (count != 0)
            {
                return false;
            }
        }
        return true;
    }
```

## Approach 2

``` C++
    bool isAnagram(string s, string t) {
        if (s.size() != t.size())
        {
            return false;
        }

        std::sort(s.begin(), s.end());
        std::sort(t.begin(), t.end());
        return s == t;
    }
```