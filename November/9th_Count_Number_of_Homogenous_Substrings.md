# Count Number of Homogenous Substrings

https://leetcode.com/problems/count-number-of-homogenous-substrings

Given a string s, return the number of homogenous substrings of s.


## Approach 
``` C++
    int countHomogenous(string s) {
        constexpr int mod = 1e9 + 7;
        int ans = 0;
        size_t curr = 0;
        while (curr < s.length())
        {
            int pivot = curr;
            size_t count = 0;
            while (curr < s.length() && s[curr] == s[pivot])
            { // Find the contiguous sequence
                count++;
                curr++;
            }
            size_t tempSum = (count * (count + 1) / 2) % mod;
            ans = (ans + tempSum) % mod;
            pivot = curr;
        }
        return ans;
    }
```