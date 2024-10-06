# Permutation in String

https://leetcode.com/problems/permutation-in-string

Given two strings s1 and s2, return true if s2 contains a 
permutation of s1, or false otherwise.

In other words, return true if one of s1's permutations is the substring of s2.

## Approach 1

``` C++
    std::vector<int> getFreq(const std::string& s, int end)
    {
        std::vector<int> freq(26, 0);
        for (int i = 0; i < end; i++)
        {
            freq[s[i] - 'a']++;
        }
        return freq;
    }

    bool checkInclusion(string s1, string s2) {
        int l1 = s1.length(), l2 = s2.length();
        if (l1 > l2)
        { // Indicates there is a character present in s1 but is not in s2.
            return false;
        }
        std::vector<int> f1 = getFreq(s1, l1);
        std::vector<int> f2 = getFreq(s2, l1);

        if (f1 == f2) return true;

        for (int prev = 0, next = l1; next < l2; prev++, next++)
        {
            f2[s2[prev] - 'a']--;
            f2[s2[next] - 'a']++;
            if (f1 == f2) return true;
        }
        return false;
    }
```

## Approach 2

Instead of checking 26 charactees evert time, matintain a variable diffCnt to track the different characters in current substring

``` C++
    bool checkInclusion(string s1, string s2) {
        int l1 = s1.length(), l2 = s2.length();
        if (l1 > l2)
        { // Indicates there is a character present in s1 but is not in s2.
            return false;
        }
        std::array<int, 26> f1{};
        std::array<int, 26> f2{};
        for (int i = 0; i < l1; i++)
        {
            f1[s1[i] - 'a']++;
            f2[s2[i] - 'a']++;
        }
        
        int diffCnt = 0;
        for (int i = 0; i < 26; i++)
        {
            diffCnt += (f1[i] != f2[i]);
        }
        if (diffCnt == 0) return true;

        for (int prev = 0, next = l1; next < l2; prev++, next++)
        {
            int p = s2[prev] - 'a', n = s2[next] - 'a';
            if (f2[p] == f1[p]) diffCnt++;
            if (f2[n] == f1[n]) diffCnt++;
            f2[p]--;
            f2[n]++;
            if (f2[p] == f1[p]) diffCnt--;
            if (f2[n] == f1[n]) diffCnt--;

            if (diffCnt == 0) return true;
        }
        return false;
    }
```
