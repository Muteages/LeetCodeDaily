# Word Break II

https://leetcode.com/problems/word-break-ii

Given a string s and a dictionary of strings wordDict, add spaces in s to construct a sentence where each word is a valid dictionary word. Return all such possible sentences in any order.

## Approach 

``` C++
    std::vector<std::string> ans;
    std::unordered_set<std::string> dict;
    int n;

    void backtrack(const std::string& s, std::string& curr, int idx)
    {
        if (idx == n)
        {
            curr.pop_back(); // Remove the last space
            ans.emplace_back(std::move(curr));
            return;
        }
        std::string word{};
        for (int i = idx; i < n; i++)
        {
            word += s[i];
            if (dict.count(word))
            { // Valid word
                std::string next = curr + word + " ";
                backtrack(s, next, i + 1);
            }
        }
    }

    vector<string> wordBreak(string s, vector<string>& wordDict) {
        ans.clear();
        std::string curr{};
        n = s.length();
        for (const auto& word : wordDict)
        {
            dict.emplace(word);
        }
        backtrack(s, curr, 0);
        return ans;
    }
```