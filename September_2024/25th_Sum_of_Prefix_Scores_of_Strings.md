# Sum of Prefix Scores of Strings

https://leetcode.com/problems/sum-of-prefix-scores-of-strings

You are given an array words of size n consisting of non-empty strings.

We define the score of a string word as the number of strings words[i] such that word is a prefix of words[i].

For example, if words = ["a", "ab", "abc", "cab"], then the score of "ab" is 2, since "ab" is a prefix of both "ab" and "abc".
Return an array answer of size n where answer[i] is the sum of scores of every non-empty prefix of words[i].

Note that a string is considered as a prefix of itself.


## Approach 1

Brute force approach:  string got TLE while string_view got AC.

``` C++
    vector<int> sumPrefixScores(vector<string>& words) {
        int n = words.size();
        std::unordered_map<std::string_view, int> prefix;
        for (const auto& word : words)
        {
            std::string_view sv = word;
            for (int len = 1; len <= sv.length(); len++)
            {
                prefix[sv.substr(0, len)]++;
            }
        }

        std::vector<int> ans(n, 0);
        for (int i = 0; i < n; i++)
        {
            std::string_view sv = words[i];
            for (int len = 1; len <= sv.length(); len++)
            {
                ans[i] += prefix[sv.substr(0, len)];
            }
        }
        return ans;
    }
```

