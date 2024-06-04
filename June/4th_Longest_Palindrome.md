# Longest Palindrome

Given a string s which consists of lowercase or uppercase letters, return the length of the longest 
palindrome
 that can be built with those letters.

Letters are case sensitive, for example, "Aa" is not considered a palindrome.


## Approach 1

``` C++
    int longestPalindrome(string s) {
        std::unordered_map<char, int> freq;
        for (char ch : s)
        {
            freq[ch]++;
        }

        int cnt = 0;
        bool hasOdd = false;
        for (auto [ch, f] : freq)
        {
            if (f % 2 == 1)
            {
                hasOdd = true;
                f -= 1;
            }
            cnt += f;
        }
        return cnt + hasOdd;
    }
```


``` JavaScript
var longestPalindrome = function(s) {
    let freq = {};
    for (let ch of s)
    {
        freq[ch] = (freq[ch] || 0) + 1;
    }
    let ans = 0;
    let hasOdd = false;
    for (let ch in freq)
    {
        let f = freq[ch];
        if (f % 2 === 1)
        {
            hasOdd = true;
            f--;
        }
        ans += f;
    }
    return ans + hasOdd;
};
```


## Approach 2

Bit manipulation approach

``` C++

    int longestPalindrome(string s) {
        uint64_t odd = 0; 
        for (char ch : s)
        {
           odd ^= 1ull << (ch - 'A');
        }
        return s.length() - __builtin_popcountll(odd) + (odd != 0);
    }
```


``` C++
    int longestPalindrome(string s) {
        std::bitset<58> freq = 0; // 'A' = 65, 'z' = 122
        for (char ch : s)
        {
            freq.flip(ch - 'A');
        }

        int odd = freq.count();
        return s.length() - odd + (odd != 0);
    }
```

## Approach 3 

``` C++
    int longestPalindrome(string s) {
        std::vector<int> freq(58, 0);
        int ans = 0;
        for (char ch : s)
        {
            int i = ch - 'A';
            if (++freq[i] % 2 == 0)
            {
                ans += 2;
            }
        }
        return (s.length() > ans) ? ans + 1 : ans;
    }
```

``` JavaScript
var longestPalindrome = function(s) {
    let ans = 0;
    let freq = {};
    for (let ch of s)
    {
        freq[ch] = (freq[ch] || 0) + 1;
        if (freq[ch] % 2 == 0)
        {
            ans += 2;
        }
    }
    return s.length > ans ? ans + 1 : ans;
};
```