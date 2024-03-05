# Minimum Length of String After Deleting Similar Ends

https://leetcode.com/problems/minimum-length-of-string-after-deleting-similar-ends

Given a string s consisting only of characters 'a', 'b', and 'c'. You are asked to apply the following algorithm on the string any number of times:

Pick a non-empty prefix from the string s where all the characters in the prefix are equal.
Pick a non-empty suffix from the string s where all the characters in this suffix are equal.
The prefix and the suffix should not intersect at any index.
The characters from the prefix and suffix must be the same.
Delete both the prefix and the suffix.
Return the minimum length of s after performing the above operation any number of times (possibly zero times).

## Approach 

``` C++
    int minimumLength(string s) {
        int l = s.length();
        int left = 0, right = l - 1;
        while (left < right && s[left] == s[right])
        {
            while (left < right - 1 && s[left] == s[left + 1])
            { // Find all same characters in prefix
                left++;
            }
            while (right > left + 1 && s[right] == s[right - 1])
            { // Find all same characters in suffix
                right--;
            }
            right--;
            left++;
        }
        return right - left + 1;
    }
```