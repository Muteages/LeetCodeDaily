# Construct K Palindrome Strings

https://leetcode.com/problems/construct-k-palindrome-strings

Given a string s and an integer k, return true if you can use all the characters in s to construct k palindrome strings or false otherwise.

## Approach 

``` C++
    bool canConstruct(string s, int k) {
        int n = s.size();
        if (n == k) return true;
        if (n < k) return false;

        std::bitset<26> freq;
        for (char ch : s)
        {
            freq[ch - 'a'].flip();
        }
        // Odd count must equal or less than k
        return freq.count() <= k;
    }
``

``` Python
    def canConstruct(self, s: str, k: int) -> bool:
        n = len(s)
        if n < k:
            return False
        if n == k:
            return True
        
        freq = [False] * 26
        for ch in s:
            freq[ord(ch) - ord('a')] ^= 1
        return freq.count(True) <= k
```

Use Counter()
``` Python
    def canConstruct(self, s: str, k: int) -> bool:
        # Alternatively, use freq := Counter(s) to use freq immdiately
        freq = Counter(s)
        return sum(f&1 for f in freq.values()) <= k <= len(s)
```


``` JavaScript
var canConstruct = function(s, k) {
    const n = s.length;
    if (k > n) return false;
    if (k === n) return true;

    let freq = new Array(26).fill(0);
    for (let ch of s) {
        freq[ch.charCodeAt() - 'a'.charCodeAt()] ^= 1;
    }

    return freq.filter(f => f === 1).length <= k;
};
```