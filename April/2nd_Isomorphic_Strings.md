# Isomorphic Strings

https://leetcode.com/problems/isomorphic-strings/

Given two strings s and t, determine if they are isomorphic.

Two strings s and t are isomorphic if the characters in s can be replaced to get t.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character, but a character may map to itself.

## Approach 1

``` C++
    bool isIsomorphic(string s, string t) {
        std::unordered_map<char, char> s2t, t2s; // Mapping form s[i] to t[i]  and t[i] to s[i]
        for (int i = 0; i < s.length(); i++)
        {
            if (!s2t.count(s[i]) && !t2s.count(t[i]))
            {
                s2t[s[i]] = t[i];
                s[i] = t[i];
                t2s[t[i]] = s[i];
            }
            else if (s2t.count(s[i]))
            {
                s[i] = s2t[s[i]];
            }
            else
            {
                return false;
            }
        }

        return s == t;
    }
```

## Approach 2

``` C++
    bool isIsomorphic(string s, string t) {
        //std::unordered_map<char, char> s2t, t2s;
        std::vector<int> s2t(128, -1), t2s(128, -1);
        for (int i = 0; i < s.length(); i++)
        {
            if (s2t[s[i]] == -1 && t2s[t[i]] == -1)
            {
                s2t[s[i]] = t[i];
                t2s[t[i]] = s[i];
            }
            else if (s2t[s[i]] != t[i] || t2s[t[i]] != s[i])
            {
                return false;
            }
        }
        return true;
    }
```

