# Append Characters to String to Make Subsequence

https://leetcode.com/problems/append-characters-to-string-to-make-subsequence

You are given two strings s and t consisting of only lowercase English letters.

Return the minimum number of characters that need to be appended to the end of s so that t becomes a subsequence of s.


## Approach 

``` JavaScript
var appendCharacters = function(s, t) {
    let sLen = s.length, tLen = t.length;
    let sIdx = 0, tIdx = 0;
    while (tIdx < tLen && sIdx < sLen)
    {
        if (s[sIdx] === t[tIdx])
        {
            tIdx++;
        }
        sIdx++;
    }
    return tLen - tIdx;
};
```