# Backspace String Compare

https://leetcode.com/problems/backspace-string-compare

Given two strings s and t, return true if they are equal when both are typed into empty text editors. '#' means a backspace character.

Note that after backspacing an empty text, the text will continue empty.


## Approach 1

Use Stack
``` C++
    void processString(std::stack<char>& st, const std::string& s)
    {
        for (auto& ch : s)
        {
            if (std::islower(ch))
            {
                st.emplace(ch);
            }
            else
            {
                if (!st.empty())
                { // backsapces a character
                    st.pop();
                }
            }
        }
    }

    bool backspaceCompare(string s, string t) {

        std::stack<char> stS, stT;
        processString(stS, s);
        processString(stT, t);

        return stS == stT;
    }
```


## Approach 2

Rebuild string in-place
``` C++
    int rebuildString(std::string& s)
    {
        int newPos = 0;
        for (char ch : s)
        {
            if (std::islower(ch))
            {
                s[newPos] = ch;
                newPos++;
            }
            else if (newPos > 0)
            {
                newPos--;
            }
        }
        return newPos;
    }

    bool backspaceCompare(string s, string t) {
        int ss = rebuildString(s);
        int tt = rebuildString(t);
        if (ss != tt)
        {
            return false;
        }

        for (int i = 0; i < ss; i++)
        {
            if (s[i] != t[i])
            {
                return false;
            }
        }
        return true;
    }
```

