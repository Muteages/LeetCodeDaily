# Make the String Great

https://leetcode.com/problems/make-the-string-great

Given a string s of lower and upper case English letters.

A good string is a string which doesn't have two adjacent characters s[i] and s[i + 1] where:

0 <= i <= s.length - 2
s[i] is a lower-case letter and s[i + 1] is the same letter but in upper-case or vice-versa.
To make the string good, you can choose two adjacent characters that make the string bad and remove them. You can keep doing this until the string becomes good.

Return the string after making it good. The answer is guaranteed to be unique under the given constraints.

## Approach 

``` C++
    bool isBadPair(const char a, const char b)
    {
        //return a != b && std::tolower(a) == std::tolower(b);
        return std::abs(a - b) == 32; // 'a' - 'A' = 32
    }
    string makeGood(string s) {
        std::string goodS{};
        for (const char& ch : s)
        {
            if (!goodS.empty() && isBadPair(goodS.back(), ch))
            {
                goodS.pop_back();
            }
            else
            {
                goodS += ch;
            }
        }
        return goodS;
    }
```