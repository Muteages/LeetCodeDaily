# Find Common Characters

https://leetcode.com/problems/find-common-characters

Given a string array words, return an array of all characters that show up in all strings within the words (including duplicates). You may return the answer in any order.


## Approach 

``` C++
    vector<string> commonChars(vector<string>& words) {
        std::vector<int> common(26, INT_MAX);
        for (const auto& word : words)
        {
            std::vector<int> freq(26, 0);
            for (char ch : word)
            {
                freq[ch - 'a']++;
            }

            for (int i = 0; i < 26; ++i)
            {
                common[i] = std::min(freq[i], common[i]);
            }
        }

        std::vector<std::string> ans;
        for (int i = 0; i < 26; ++i)
        {
            for (int j = 0; j < common[i]; ++j)
            {
                ans.emplace_back(std::string(1, i + 'a'));
            }
        }
        return ans;
    }
```


``` JavaScript
var commonChars = function(words) {
    let ans = [];

    for (const ch of words[0])
    {
        if (words.every((word) => word.includes(ch))) {
            ans.push(ch);
            words = words.map((word) => word.replace(ch, ""));
        }
    }
    return ans;
};
```