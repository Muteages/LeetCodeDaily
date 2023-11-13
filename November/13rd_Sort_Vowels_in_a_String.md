# Sort Vowels in a String

https://leetcode.com/problems/sort-vowels-in-a-string

Given a 0-indexed string s, permute s to get a new string t such that:

All consonants remain in their original places.
The vowels must be sorted in the nondecreasing order of their ASCII values.
Return the resulting string.

## Approach 

``` C++
    string sortVowels(string s) {
        std::vector<int> position; // Record all vowels positions
        std::vector<char> vowels; // Record all vowels;
        const std::string compare = "aeiouAEIOU";
        for (int i = 0; i < s.length(); i++)
        {
            if (compare.find(s[i]) != std::string::npos)
            {
                position.emplace_back(i);
                vowels.emplace_back(s[i]);
            }
        }

        std::sort(vowels.begin(), vowels.end());
        for (int i = 0; i < position.size(); i++)
        {
            s[position[i]] = vowels[i];
        }
        return s;
    }
```