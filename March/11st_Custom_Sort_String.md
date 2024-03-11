# Custom Sort String

https://leetcode.com/problems/custom-sort-string

You are given two strings order and s. All the characters of order are unique and were sorted in some custom order previously.

Permute the characters of s so that they match the order that order was sorted. More specifically, if a character x occurs before a character y in order, then x should occur before y in the permuted string.

Return any permutation of s that satisfies this property.


## Approach 

``` C++
    string customSortString(string order, string s) {
        std::vector<int> freq(26, 0);
        for (char ch : s)
        {
            freq[ch - 'a']++;
        }

        std::string ans{};
        for (char ch : order)
        {
            if (freq[ch - 'a'] > 0)
            {
                ans += std::string(freq[ch - 'a'], ch);
                freq[ch - 'a'] = 0;
            }
        }
        for (int i = 0; i < 26; i++)
        {
            if (freq[i] > 0)
            {
                ans += std::string(freq[i], static_cast<char>(i + 'a'));
            }
        }
        return ans;
    }
```