# Minimum Remove to Make Valid Parentheses

https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses

Given a string s of '(' , ')' and lowercase English characters.

Your task is to remove the minimum number of parentheses ( '(' or ')', in any positions ) so that the resulting parentheses string is valid and return any valid string.

Formally, a parentheses string is valid if and only if:

It is the empty string, contains only lowercase characters, or
It can be written as AB (A concatenated with B), where A and B are valid strings, or
It can be written as (A), where A is a valid string.

## Approach 1

``` C++
    string minRemoveToMakeValid(string s) {
        int len = s.length();
        int brackets = 0;
        for (int i = len - 1; i >= 0; i--)
        {
            brackets += (s[i] == '(') - (s[i] == ')'); 
            if (brackets > 0)
            {
                s[i] = '#';
                brackets = 0;
            }
        }

        brackets = 0;
        for (int i = 0; i < len; i++)
        {
            brackets += (s[i] == '(') - (s[i] == ')'); 
            if (brackets < 0)
            {
                s[i] = '#';
                brackets = 0;
            }
        }
        auto it = std::remove(s.begin(), s.end(), '#');
        s.erase(it, s.end());
        return s;
    }
```

## Approach 2

Finished  in two passes
``` C++
    string minRemoveToMakeValid(string s) {
        int len = s.length();
        int brackets = 0;
        for (int i = len - 1; i >= 0; i--)
        {
            brackets += (s[i] == '(') - (s[i] == ')'); 
            if (brackets > 0)
            {
                s[i] = '#';
                brackets = 0;
            }
        }

        brackets = 0;
        int sz = len;
        for (int i = 0, idx = 0; i < len; i++)
        {
            brackets += (s[i] == '(') - (s[i] == ')');
            if (s[i] != '#' && brackets >= 0)
            { // Rewrite the string in place
                s[idx++] = s[i]; 
            }
            else 
            {
                sz--;
                brackets = 0;
            }
        }
        s.resize(sz);
        return s;
    }
```

