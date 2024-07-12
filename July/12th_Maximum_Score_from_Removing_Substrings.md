# Maximum Score from Removing Substrings

https://leetcode.com/problems/maximum-score-from-removing-substrings

You are given a string s and two integers x and y. You can perform two types of operations any number of times.

Remove substring "ab" and gain x points.
For example, when removing "ab" from "cabxbae" it becomes "cxbae".
Remove substring "ba" and gain y points.
For example, when removing "ba" from "cabxbae" it becomes "cabxe".
Return the maximum points you can gain after applying the above operations on s.


## Approach 

``` C++
    void removeSub(const std::string& s, std::stack<char>& st, const std::string pattern, int points, int& ans)
    {
        char first = pattern[0], second = pattern[1];
        for (const char ch : s)
        {
            if (ch == second && !st.empty() && st.top() == first)
            {
                st.pop();
                ans += points;
            }
            else
            {
                st.emplace(ch);
            }
        }
    }

    std::string rebuild(std::stack<char>& st)
    {
        std::string s{};
        while (!st.empty())
        {
            s += st.top();
            st.pop();
        }
        std::reverse(s.begin(), s.end());
        return s;
    }

    int maximumGain(string s, int x, int y) {
        std::stack<char> st;
        int ans = 0;
        if (x > y)
        {
            removeSub(s, st, "ab", x, ans);
            s = rebuild(st);
            removeSub(s, st, "ba", y, ans);
        }
        else
        {
            removeSub(s, st, "ba", y, ans);
            s = rebuild(st);
            removeSub(s, st, "ab", x, ans);
        }
        return ans;
    }
```

## Approach 2

Without the extra stack, modift the string in place

``` C++
    int removeSub(std::string& s, char* pattern, int points)
    {
        char first = pattern[0], second = pattern[1];
        int idx = 0, ans = 0;
        for (char ch : s)
        {
            s[idx++] = ch;
            if (idx > 1 && s[idx - 2] == first && s[idx - 1] == second)
            {
                idx -= 2;
                ans += points;
            }
        }
        s.resize(idx);
        return ans;
    }


    int maximumGain(string s, int x, int y) {
        char first[3] = "ab", second[3] = "ba";
        if (x < y)
        {
            std::swap(x, y);
            std::swap(first, second);
        }
        return removeSub(s, first, x) + removeSub(s, second, y);
    }
```

## Approach 3

``` JavaScript
var maximumGain = function(s, x, y) {
    let first = 'a', second = 'b';
    if (x < y) {
        [x, y, first, second] = [y, x, second, first];
    }
    let fCnt = 0, sCnt = 0, ans = 0;
    for (let ch of s) {
        if (ch === first) {
            fCnt++;
        }
        else if (ch === second) {
            if (fCnt) {
                ans += x;
                fCnt--;
            }
            else {
                sCnt++;
            }
        }
        else {
            ans += y * Math.min(fCnt, sCnt);
            fCnt = 0;
            sCnt = 0;
        }
    }
    ans += y * Math.min(fCnt, sCnt); // final round
    return ans;
};
```