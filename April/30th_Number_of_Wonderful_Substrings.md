# Number of Wonderful Substrings

https://leetcode.com/problems/number-of-wonderful-substrings

A wonderful string is a string where at most one letter appears an odd number of times.

For example, "ccjjc" and "abab" are wonderful, but "ab" is not.
Given a string word that consists of the first ten lowercase English letters ('a' through 'j'), return the number of wonderful non-empty substrings in word. If the same substring appears multiple times in word, then count each occurrence separately.


## Approach 

``` C++
    long long wonderfulSubstrings(string& word) {
        int n = word.length();
        long long cnt = 0;
        uint16_t freq[1024] = {0};
        freq[0] = 1;
        uint16_t sum = 0;
        for(char ch : word)
        {
            int idx = ch -'a';
            sum ^= (1<<idx);
            cnt += freq[sum]++;
            for(int i = 0; i < 10; i++)
            {
                cnt += freq[sum ^ (1<<i)];
            }
        }
        return cnt;
    }
```