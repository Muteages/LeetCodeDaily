# Decoded String at Index

https://leetcode.com/problems/decoded-string-at-index

You are given an encoded string s. To decode the string to a tape, the encoded string is read one character at a time and the following steps are taken:

If the character read is a letter, that letter is written onto the tape.
If the character read is a digit d, the entire current tape is repeatedly written d - 1 more times in total.
Given an integer k, return the kth letter (1-indexed) in the decoded string.

## Approach 1
``` C++
    string decodeAtIndex(string s, int k) {
        size_t len = 0;
        // Calculate the total length
        for (auto& ch : s)
        {
            if (std::islower(ch))
            {
                len++;
            }
            else
            {
                len *= (ch - '0');
            }
        }

        for (size_t i = s.length() - 1; i >= 0; i--)
        {
            if (std::isdigit(s[i]))
            { // Adjust the length
                len /= (s[i] - '0');
                k = k % len; // Indicates that the target is the kth letter at current substring
            }
            else
            { // Find the letter
                if (len == k || k == 0)
                {
                    return std::string(1, s[i]);
                }
                len--;
            }
        }
        return " ";
    }
```

## Approach 2

Instead reverse from the end of the string, find the minimum suitable substring

``` C++
   string decodeAtIndex(string s, int k) {
        size_t len = 0;
        int curPos = -1; // Record the stop position at s
        while (len < k)
        { // Calculate the total length
            curPos++;
            if (std::islower(s[curPos]))
            {
                len++;
            }
            else
            {
                len *= (s[curPos] - '0');
            }
        }

        for (int i = curPos; i >= 0; i--)
        {
            if (std::isdigit(s[i]))
            { // Adjust the length
                len /= (s[i] - '0');
                k = k % len; // Indicates that the target is the kth letter in current substring
            }
            else
            { // Find the letter
                if (len == k || k == 0)
                {
                    return std::string(1, s[i]);
                }
                len--;
            }
        }
        return " ";
    }
```