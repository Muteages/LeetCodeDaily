# Count the Number of Consistent Strings

https://leetcode.com/problems/count-the-number-of-consistent-strings

You are given a string allowed consisting of distinct characters and an array of strings words. A string is consistent if all characters in the string appear in the string allowed.

Return the number of consistent strings in the array words.

## Approach 

``` JavaScript
var countConsistentStrings = function(allowed, words) {
    let s = new Set(allowed);

    const isConsistent = (word) => {
        for (let ch of word) {
            if (!s.has(ch)) {
                return false;
            }
        }
        return true;
    };

    let ans = 0;
    for (let word of words) {
        if (isConsistent(word)) {
            ans++;
        }
    }
    return ans;
};
```

``` C++
    int countConsistentStrings(string allowed, vector<string>& words) {
        std::bitset<26> s{};
        for (const char ch : allowed) 
        {
            s[ch - 'a'] = 1;
        }

        int ans = 0;
        for (const auto& word : words)
        {
            int cnt = 1;
            for (const char ch : word) 
            {
                if (!s[ch - 'a']) 
                {
                    cnt = 0;
                    break;
                }
            }
            ans += cnt;
        }
        return ans;
    }
```