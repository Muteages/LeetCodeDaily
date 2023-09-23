# Longest String Chain

https://leetcode.com/problems/longest-string-chain

You are given an array of words where each word consists of lowercase English letters.

wordA is a predecessor of wordB if and only if we can insert exactly one letter anywhere in wordA without changing the order of the other characters to make it equal to wordB.

For example, "abc" is a predecessor of "abac", while "cba" is not a predecessor of "bcad".
A word chain is a sequence of words [word1, word2, ..., wordk] with k >= 1, where word1 is a predecessor of word2, word2 is a predecessor of word3, and so on. A single word is trivially a word chain with k == 1.

Return the length of the longest possible word chain with words chosen from the given list of words.


## Approach 

``` C++
    int longestStrChain(vector<string>& words) {
        if (words.size() == 1)
        {
            return 1;
        }

        std::sort(words.begin(), words.end(), 
            [](const std::string& s1, const std::string& s2)
            { // Sort the words by the length of each word
                return s1.length() < s2.length();
            });

        int cnt = 0;
        std::unordered_map<std::string, int> ump;
        for (const auto& word : words)
        {
            int longest = 1; // Counting self as 1
            for (size_t i = 0; i < word.length(); i++)
            {
                /*
                std::string sub = word.substr(0, i) + word.substr(i + 1);
                if (ump.find(sub) != ump.end())
                {
                    ump[word] = std::max(ump[word], ump[sub] + 1);
                }
                */
                std::string sub = word;
                sub.erase(i, 1);
                longest = std::max(longest, ump[sub] + 1);
            }
            // Update
            ump[word] = longest;
            cnt = std::max(cnt, longest);
        }
        return cnt;
    }
```