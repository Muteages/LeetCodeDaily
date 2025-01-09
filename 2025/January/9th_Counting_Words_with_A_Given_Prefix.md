# Counting Words with A Given Prefix

https://leetcode.com/problems/counting-words-with-a-given-prefix

You are given an array of strings words and a string pref.

Return the number of strings in words that contain pref as a prefix.

A prefix of a string s is any leading contiguous substring of s.

## Approach 

``` C++
    int prefixCount(vector<string>& words, string pref) {
        int ans = 0;
        for (const auto& word : words)
        {
            ans += word.starts_with(pref);
        }
        return ans;
    }
```

``` JavaScript
var prefixCount = function(words, pref) {
    return words.reduce(
        (cnt, word) => cnt + word.startsWith(pref), 0);
};
```

``` Python
    def prefixCount(self, words: List[str], pref: str) -> int:
        return sum(word.startswith(pref) for word in words)
```