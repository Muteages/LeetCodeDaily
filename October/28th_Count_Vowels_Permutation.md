# Count Vowels Permutation

https://leetcode.com/problems/count-vowels-permutation

Given an integer n, your task is to count how many strings of length n can be formed under the following rules:

Each character is a lower case vowel ('a', 'e', 'i', 'o', 'u')
Each vowel 'a' may only be followed by an 'e'.
Each vowel 'e' may only be followed by an 'a' or an 'i'.
Each vowel 'i' may not be followed by another 'i'.
Each vowel 'o' may only be followed by an 'i' or a 'u'.
Each vowel 'u' may only be followed by an 'a'.
Since the answer may be too large, return it modulo 10^9 + 7.

## Approach
``` C++
    const int mod = 1e9 + 7;
    int countVowelPermutation(int n) {

        // Or just 5 variables to record the counts
        std::vector<int64_t> prevCnt(5, 1); // Indicates the count with the string end with a, e, i, o, u respectively
        std::vector<int64_t> currCnt(5, 0);
        /*    currCnt |   prevCnt 
            0 a       =   e + i + u
            1 e       =   a + i
            2 i       =   e + o
            3 o       =   i
            4 u       =   i + o
        */ 

        while (n > 1) // Remove the initial row. i.e: n == 1
        {
            currCnt[0] = (prevCnt[1] + prevCnt[2] + prevCnt[4]) % mod;
            currCnt[1] = (prevCnt[0] + prevCnt[2]) % mod;
            currCnt[2] = (prevCnt[1] + prevCnt[3]) % mod;
            currCnt[3] = prevCnt[2] % mod;
            currCnt[4] = (prevCnt[2] + prevCnt[3]) % mod;

            // Update 
            prevCnt = currCnt;
            n--;
        }

        int ans = 0;
        for (auto cnt : prevCnt)
        {
            ans = (ans + cnt) % mod;
        }
        return ans;
    }
```