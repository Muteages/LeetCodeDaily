# Largest Odd Number in String

https://leetcode.com/problems/largest-odd-number-in-string

You are given a string num, representing a large integer. Return the largest-valued odd integer (as a string) that is a non-empty substring of num, or an empty string "" if no odd integer exists.

## Apporach

``` C++
    string largestOddNumber(string num) {
        std::string ans{};
        for (int i = num.length() - 1; i >= 0; i--)
        {
            if ((num[i] - '0') % 2 != 0)
            { // Odd 
                ans = num.substr(0, i + 1);
                break;
            }
        }
        return ans;
    }
```

