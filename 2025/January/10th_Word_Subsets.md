# Word Subsets

https://leetcode.com/problems/word-subsets

You are given two string arrays words1 and words2.

A string b is a subset of string a if every letter in b occurs in a including multiplicity.

For example, "wrr" is a subset of "warrior" but is not a subset of "world".
A string a from words1 is universal if for every string b in words2, b is a subset of a.

Return an array of all the universal strings in words1. You may return the answer in any order.

## Approach 

``` C++
    void countFrequency(const std::string& s, std::vector<int>& freq)
    {
        for (char ch : s)
        {
            freq[ch - 'a']++;
        }
    }

    void updateRequiredFreq(std::vector<int>& requiredFreq, const std::vector<int>& freq)
    {
        for (int i = 0; i < 26; i++)
        {
            requiredFreq[i] = std::max(requiredFreq[i], freq[i]);
        }
    }

    bool isUniversal(const std::vector<int>& txt, const std::vector<int>& pat)
    {
        for (int i = 0; i < 26; i++)
        {
            if (txt[i] < pat[i])
            {
                return false;
            }
        }
        return true;
    }

    vector<string> wordSubsets(vector<string>& words1, vector<string>& words2) {
        std::vector<std::string> ans{};

        std::vector<int> requiredFreq(26, 0);
        for (const auto& word : words2)
        {
            std::vector<int> temp(26, 0);
            countFrequency(word, temp);
            updateRequiredFreq(requiredFreq, temp);
        }

        for (const auto& word : words1)
        {
            std::vector<int> wFreq(26, 0);
            countFrequency(word, wFreq);
            if (isUniversal(wFreq, requiredFreq))
            {
                ans.emplace_back(word);
            }
        }
        return ans;
    }
```