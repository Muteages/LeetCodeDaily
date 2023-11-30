# Maximum Number of Vowles in a Substring of Given Length

https://leetcode.com/problems/maximum-number-of-vowels-in-a-substring-of-given-length

Given a string s and an integer k, return the maximum number of vowel letters in any substring of s with length k.

## Approach 1

Brute force

``` C++
    int maxVowels(string s, int k) {
        std::string vowels = "aeiou";
        int left = 0;
        int ans = 0;
        while (left <= s.length() - k)
        {
            int curCount = 0;
            int right = left + k;
            for (int i = left; i < right; i++)
            {
                if (vowels.find(s[i]) != std::string::npos)
                {
                    curCount++;
                }
            }
            ans = std::max(ans, curCount);
            left++;
        }
        return ans;
    }
```

## Approach 2

``` C++
    int maxVowels(string s, int k) {
        std::string vowels = "aeiou";
        int curCount = 0;
        // Initialise
        for (int i = 0; i < k; i++)
        {
            if (vowels.find(s[i]) != std::string::npos)
            {
                curCount++;
            }
        }
        int ans = curCount;
        int curTail = k;
        while (curTail < s.length())
        {
            // Add the new tail and remove the old head
            if (vowels.find(s[curTail]) != std::string::npos)
            {
                curCount++;
            }
            if (vowels.find(s[curTail - k]) != std::string::npos)
            {
                curCount--;
            }
            curTail++;
            ans = std::max(ans, curCount);
        }

        return ans;
    }
```