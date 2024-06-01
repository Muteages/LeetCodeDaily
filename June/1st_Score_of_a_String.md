# Score of a String

You are given a string s. The score of a string is defined as the sum of the absolute difference between the ASCII values of adjacent characters.

Return the score of s.

## Approach

``` C++
    int scoreOfString(string s) {
        int ans = 0;
        for (int i = 0; i < s.length() - 1; i++)
        {
            ans += std::abs(s[i] - s[i + 1]);
        }
        return ans;
    }
```

``` JavaScript
var scoreOfString = function(s) {
    let ans = 0;
    for (let i = 0; i < s.length - 1; i++)
    {
        ans += Math.abs(s.charCodeAt(i) - s.charCodeAt(i + 1));
    }
    return ans;
```