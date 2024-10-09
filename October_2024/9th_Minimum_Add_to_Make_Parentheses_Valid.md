# Minimum Add to Make Parentheses Valid

https://leetcode.com/problems/minimum-add-to-make-parentheses-valid

A parentheses string is valid if and only if:

It is the empty string,
It can be written as AB (A concatenated with B), where A and B are valid strings, or
It can be written as (A), where A is a valid string.
You are given a parentheses string s. In one move, you can insert a parenthesis at any position of the string.

For example, if s = "()))", you can insert an opening parenthesis to be "(()))" or a closing parenthesis to be "())))".
Return the minimum number of moves required to make s valid.


## Approach 1

``` C++
    int minAddToMakeValid(string s) {
        std::stack<char> st{};
        for (const char ch : s) 
        {
            if (!st.empty() && st.top() == '(' && ch == ')')
            {
                st.pop();
            }
            else
            {
                st.emplace(ch);
            }
        }
        return st.size();
    }
```

## Approach 

Avoid extra stack, just use a variable to track existing opening parentheses and unparenthesized characters.

``` C++
    int minAddToMakeValid(string s) {
        int open = 0, close = 0;
        for (const char ch : s)
        {
            if (ch == '(')
            {
                open++;
            }
            else if (open > 0)
            {
                open--;
            }
            else
            {
                close++;
            }
        }
        return open + close;
    }
```

Simulate the stack process
``` C++
   int minAddToMakeValid(string s) {
        int open = 0, unvalid = 0;
        for (const char ch : s)
        {
            if (unvalid != 0 && open > 0 && ch == ')')
            {
                open--;
                unvalid--;
            }
            else if (ch == ')')
            {
                open = 0;
                unvalid++;
            }
            else
            {
                open++;
                unvalid++;
            }
        }
        return unvalid;
    }
```