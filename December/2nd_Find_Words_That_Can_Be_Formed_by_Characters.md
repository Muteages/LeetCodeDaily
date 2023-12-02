# Find Words That Can Be Formed by Characters

https://leetcode.com/problems/find-words-that-can-be-formed-by-characters

You are given an array of strings words and a string chars.

A string is good if it can be formed by characters from chars (each character can only be used once).

Return the sum of lengths of all good strings in words.

## Approach 

We can use vector or unordered_map to store the frequencies but vector way is better and cost less.
``` C++
    bool isGood(std::vector<int> freq, const std::string s)
    {
        for (const char& ch : s)
        {
            freq[ch - 'a']--;
            if (freq[ch - 'a'] < 0)
            {
                return false;
            }
        }
        return true;
    }
    int countCharacters(vector<string>& words, string chars) {
        std::vector<int> freq(26, 0); 
        for (const char& ch : chars)
        {
            freq[ch - 'a']++;
        }

        int ans = 0;
        for (const auto& word : words)
        {
            if (isGood(freq, word))
            {
                ans += word.length();
            }
        }
        return ans;
    }
```