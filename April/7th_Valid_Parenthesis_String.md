# Valid Parenthesis String

https://leetcode.com/problems/valid-parenthesis-string

Given a string s containing only three types of characters: '(', ')' and '*', return true if s is valid.

The following rules define a valid string:

Any left parenthesis '(' must have a corresponding right parenthesis ')'.
Any right parenthesis ')' must have a corresponding left parenthesis '('.
Left parenthesis '(' must go before the corresponding right parenthesis ')'.
'*' could be treated as a single right parenthesis ')' or a single left parenthesis '(' or an empty string "".


## Approach 1

Utilise 2 passes to check if backets are paired
``` C++
    bool checkValidString(string s) {
        int brackets = 0;
        int starNum = 0;
        int len = s.length();
        for (int i = 0; i < len; i++)
        {
            brackets += (s[i] == '(') - (s[i] == ')');
            starNum += (s[i] == '*');
            if (brackets < 0)
            {
                if (starNum > 0)
                {
                    brackets = 0;
                    starNum--;
                }
                else 
                {
                    return false;
                }
            }
        }

        brackets = 0;
        starNum = 0;
        for (int i = len - 1; i >= 0; i--)
        {
            brackets += (s[i] == ')') - (s[i] == '(');
            starNum += (s[i] == '*');
            if (brackets < 0)
            {
                if (starNum > 0)
                {
                    brackets = 0;
                    starNum--;
                }
                else 
                {
                    return false;
                }
            }
        }
        return true;
    }
```

## Approach 2

Greedy

``` C++
    bool checkValidString(string s) {
        if (s.back() == '(')
        {
            return false;
        }
        int maxOpen = 0, minOpen = 0;
        for (char ch : s)
        {
            if (ch == '(')
            {
                maxOpen++;
                minOpen++;
            }
            else if (ch == ')')
            {
                maxOpen--;
                minOpen--;
            }
            else
            { // ch == '*'
                maxOpen++;
                minOpen--;
            }
            if (maxOpen < 0)
            {
                return false;
            }
            minOpen = std::max(minOpen, 0);
        }
        return minOpen == 0;
    }
```