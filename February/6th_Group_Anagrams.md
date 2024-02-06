# Group Anagrams

https://leetcode.com/problems/group-anagrams

Given an array of strings strs, group the anagrams together. You can return the answer in any order.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

## Approach 

``` C++
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        std::unordered_map<std::string, std::vector<std::string>> ump;
        for (const auto& str : strs)
        {
            std::string pattern = str;
            std::sort(pattern.begin(), pattern.end());
            ump[pattern].emplace_back(str);
        }

        std::vector<std::vector<std::string>> ans;
        for (const auto& [str, anagrams] : ump)
        {
            ans.emplace_back(anagrams);
        }
        return ans;
    }
```
