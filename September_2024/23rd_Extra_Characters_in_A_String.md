# Extra Characters in a String

https://leetcode.com/problems/extra-characters-in-a-string

You are given a 0-indexed string s and a dictionary of words dictionary. You have to break s into one or more non-overlapping substrings such that each substring is present in dictionary. There may be some extra characters in s which are not present in any of the substrings.

Return the minimum number of extra characters left over if you break up s optimally.

## Approach 1

From head to tail

``` JavaScript
var minExtraChar = function(s, dictionary) {
    const len = s.length;
    const dp = [0];

    for (let i = 1; i <= len; i++) {
        dp.push(dp[i - 1] + 1);
        for (let word of dictionary) {
            let wl = word.length;
            if (i >= wl && s.slice(i - wl, i) == word) {
                dp[i] = Math.min(dp[i], dp[i - wl]);
            }
        }
    }
    return dp[len];
};
```

## Approach 2

From tail to head

``` JavaScript
var minExtraChar = function(s, dictionary) {
    const len = s.length;
    const dp = new Array(len + 1).fill(Infinity);
    dp[len] = 0;

    for (let i = len - 1; i >= 0; i--) {
        dp[i] = dp[i + 1] + 1; // Assume the character s[i] is an extra character first.     
        for (let word of dictionary) {
            let l = word.length;
            if (i + l <= len && s.slice(i, i + l) == word) { 
                // If find a word in dictionary, update the array
                dp[i] = Math.min(dp[i], dp[i + l]);
            }
        }
    }
    return dp[0];
};
```

## Approach 3

Use string_view to avoid creating new substrings

``` C++
    int minExtraChar(string s, vector<string>& dictionary) {
        int len = s.length();
        std::vector<int> dp(len + 1, INT_MAX);
        dp[len] = 0;
        std::string_view sv(s);
        std::unordered_set<std::string_view> us(dictionary.begin(), dictionary.end());

        for (int i = len - 1; i >= 0; i--)
        {
            dp[i] = dp[i + 1] + 1;
            for (int j = i + 1; j <= len; j++)
            {
                auto sub = sv.substr(i, j - i);
                if (us.count(sub))
                {
                    dp[i] = std::min(dp[i], dp[j]);
                }
            }
        }
        return dp[0];
    }
```