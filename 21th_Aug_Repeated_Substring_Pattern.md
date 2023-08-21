# Repeated Substring Pattern

https://leetcode.com/problems/repeated-substring-pattern/description/

Given a string s, check if it can be constructed by taking a substring of it and appending multiple copies of the substring together.

## Approach 1

Rotate the string 

``` C++
    bool repeatedSubstringPattern(string s) {
        size_t len = s.length();
        std::string tempString = s;
        for (size_t count = 0; count < len / 2; count++)
        { // left shift the string, if it can be constructed by its substring, the new string will equal to s after n times(substring length but less than itself) rotations.
            char tempCh = tempString[0];
            tempString = tempString.substr(1) + tempCh;
            if (tempString == s)
            {
                return true;
            }
        }
        return false;
    }
```

## Approach 2 

Double string and remove the head and tail. If the potential substring exists, we can find s in the new string.

``` C++
    bool repeatedSubstringPattern(string s) {
        std::string copied = s + s;
        copied = copied.substr(1, copied.length() - 2);
        return copied.find(s) != std::string::npos;
    }
```

