# Minimum Deletions to Make String Balanced

https://leetcode.com/problems/minimum-deletions-to-make-string-balanced

You are given a string s consisting only of characters 'a' and 'b'​​​​.

You can delete any number of characters in s to make s balanced. s is balanced if there is no pair of indices (i,j) such that i < j and s[i] = 'b' and s[j]= 'a'.

Return the minimum number of deletions needed to make s balanced.

## Approach 1 

2 passes with O(n) space complexity.

``` C++
    int minimumDeletions(string s) {
        const int n = s.length();
        std::vector<int> prefix(n, 0), suffix(n, 0); // preifx "b"s and suffix "a"s
        for (int i = 1; i < n; i++)
        {
            prefix[i] = prefix[i - 1] + (s[i - 1] == 'b');
            suffix[n - i - 1] = suffix[n - i] + (s[n - i] == 'a');
        }

        int ans = n;
        for (int i = 0; i < n; i++)
        {
            ans = std::min(ans, prefix[i] + suffix[i]);
        }
        return ans;
    }
```
## Approach 2

2 passes with O(1) space complexity.

``` JavaScript
var minimumDeletions = function(s) {
    let n = s.length;
    let aCnt = 0, bCnt = (s[0] === 'b');
    for (let ch of s) {
        aCnt += (ch === 'a');
    }
    let ans = aCnt + bCnt - 1;
    for (let i = 1; i < n; i++) {
        aCnt -= (s[i - 1] === 'a');
        bCnt += (s[i] === 'b');
        ans = Math.min(ans, aCnt + bCnt - 1);
    }
    return ans;
};
```

## Approach 3

2 pass with O(1) space complexity.

``` JavaScript
var minimumDeletions = function(s) {
    let n = s.length;
    let aCnt = 0, bCnt = (s[0] === 'b');
    for (let ch of s) {
        aCnt += (ch === 'a');
    }
    let ans = aCnt + bCnt - 1;
    for (let i = 1; i < n; i++) {
        aCnt -= (s[i - 1] === 'a');
        bCnt += (s[i] === 'b');
        ans = Math.min(ans, aCnt + bCnt - 1);
    }
    return ans;
};
```

## Approach 4

1 pass with O(1) space complexity.

``` JavaScript
var minimumDeletions = function(s) {
    let n = s.length;
    let bCnt = 0, ans = 0;
    for (let ch of s) {
        if (ch === 'a') {
            ans = Math.min(ans + 1, bCnt); // Decide whether to delete the current 'a'(+ 1) or all "b"s
        }
        else {
            bCnt++;
        }
    }
    return ans;
};
```