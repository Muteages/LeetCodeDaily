# Largest 3 Same Digit Number in String

https://leetcode.com/problems/largest-3-same-digit-number-in-string

You are given a string num representing a large integer. An integer is good if it meets the following conditions:

It is a substring of num with length 3.
It consists of only one unique digit.
Return the maximum good integer as a string or an empty string "" if no such integer exists.

Note:

A substring is a contiguous sequence of characters within a string.
There may be leading zeroes in num or a good integer.

## Approach 1

Traverse the string

``` C++
    string largestGoodInteger(string num) {
        std::string ans{};
        for (int i = 0; i <= num.length() - 3; i++)
        {
            if (num[i] == num[i + 1] && num[i] == num[i + 2])
            {
                if (ans.empty())
                { // Initialise
                    ans = num.substr(i, 3);
                }
                else if (num[i] > ans.back())
                {
                    ans = num.substr(i, 3);
                }
            }
        }
        return ans;
    }
```

## Approach 2

Find potential subsequence

``` C++
    string largestGoodInteger(string num) {
        for (int i = 9; i >= 0; i--)
        {
            std::string c = std::to_string(i);
            std::string s = c + c + c;
            if (num.find(s) != std::string::npos)
            {
                return s;
            }
        }
        return "";
    }
```