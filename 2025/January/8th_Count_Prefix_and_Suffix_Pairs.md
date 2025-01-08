# Count Prefix and Suffix Pairs


https://leetcode.com/problems/count-prefix-and-suffix-pairs-i

ou are given a 0-indexed string array words.

Let's define a boolean function isPrefixAndSuffix that takes two strings, str1 and str2:

isPrefixAndSuffix(str1, str2) returns true if str1 is both a 
prefix
 and a 
suffix
 of str2, and false otherwise.
For example, isPrefixAndSuffix("aba", "ababa") is true because "aba" is a prefix of "ababa" and also a suffix, but isPrefixAndSuffix("abc", "abcd") is false.

Return an integer denoting the number of index pairs (i, j) such that i < j, and isPrefixAndSuffix(words[i], words[j]) is true.

## Approach 1

Basic compare or string_view
``` C++
    int countPrefixSuffixPairs(vector<string>& words) {
        int n = words.size();
        int ans = 0;
        for (int i = 0; i < n; i++)
        {
            for (int j = i + 1; j < n; j++)
            {
                ans += isPrefixAndSuffix(words[i], words[j]);
            }
        }
        return ans;
    }
    /*
    bool isPrefixAndSuffix(std::string_view pat, std::string_view txt)
    {
        int pLen = pat.length(), tLen = txt.length();
        if (pLen > tLen) return false;
        return (txt.substr(0, pLen) == pat) && (txt.substr(tLen - pLen) == pat);
    }
    */
    bool isPrefixAndSuffix(const std::string& pat, const std::string& txt)
    {
        int pLen = pat.length(), tLen = txt.length();
        if (pLen > tLen) return false;
        int pl = 0, pr = pLen - 1;
        int tl = 0, tr = tLen - 1;
        while (pl < pLen && pr >= 0)
        {
            if (pat[pl++] != txt[tl++] || pat[pr--] != txt[tr--])
            {
                return false;
            }
        }
        return true;
    }
```

## Approach 2

C++ 20 built-in prefix and suffix check functions

``` C++
    int countPrefixSuffixPairs(vector<string>& words) {
        int n = words.size();
        int ans = 0;
        for (int i = 0; i < n; i++)
        {
            for (int j = i + 1; j < n; j++)
            {
                ans += (words[j].starts_with(words[i]) && words[j].ends_with(words[i]));
            }
        }
        return ans;
    }
```

``` JavaScript
var countPrefixSuffixPairs = function(words) {
    const n = words.length;
    let ans = 0;
    for (let i = 0; i < n; i++) {
        for (let j = i + 1; j < n; j++) {
            ans += words[j].startsWith(words[i]) && words[j].endsWith(words[i]);
        }
    }
    return ans;
};
```

``` Python
    def countPrefixSuffixPairs(self, words: List[str]) -> int:
        ans = 0

        for i in range(len(words)):
            for j in range(i + 1, len(words)):
                ans += words[j].startswith(words[i]) and words[j].endswith(words[i])
        
        return ans
```






