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