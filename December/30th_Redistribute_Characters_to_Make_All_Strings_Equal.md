# Redistribute Characters to Make All Strings Equal

https://leetcode.com/problems/redistribute-characters-to-make-all-strings-equal

You are given an array of strings words (0-indexed).

In one operation, pick two distinct indices i and j, where words[i] is a non-empty string, and move any character from words[i] to any position in words[j].

Return true if you can make every string in words equal using any number of operations, and false otherwise.

 
## Approach 

``` C++
    bool makeEqual(vector<string>& words) {
        std::unordered_map<char, int> freq;
        for (const auto& word : words)
        {
            for (const auto& ch : word)
            {
                freq[ch]++;
            }
        }
        int n = words.size();
        for (const auto& [ch, f] : freq)
        {
            if (f % n != 0)
            {
                return false;
            }
        }
        return true;
    }
```