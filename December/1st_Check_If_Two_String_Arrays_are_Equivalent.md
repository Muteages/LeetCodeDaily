# Check If Two String Arrays are Equivalent

https://leetcode.com/problems/check-if-two-string-arrays-are-equivalent

Given two string arrays word1 and word2, return true if the two arrays represent the same string, and false otherwise.

## Approach 1

Concatenate two string.

``` C++
    bool arrayStringsAreEqual(vector<string>& word1, vector<string>& word2) {
        std::string s1 = "", s2 = "";
        for (const auto& s : word1)
        {
            s1 += s;
        }
        for (const auto& s : word2)
        {
            s2 += s;
        }
        return s1 == s2;
    }
```

## Approach 2
``` C++
    bool arrayStringsAreEqual(vector<string>& word1, vector<string>& word2) {
        int idx1 = 0, idx2 = 0;
        int curr1 = 0, curr2 = 0;
        while (idx1 < word1.size() && idx2 < word2.size())
        {
            char ch1 = word1[idx1][curr1];
            char ch2 = word2[idx2][curr2];

            if (ch1 != ch2)
            {
                return false;
            }

            curr1++;
            curr2++;

            if (curr1 == word1[idx1].size())
            {
                curr1 = 0;
                idx1++;
            }
            if (curr2 == word2[idx2].size())
            {
                curr2 = 0;
                idx2++;
            }
        }

        return idx1 == word1.size() && idx2 == word2.size();
    }
```