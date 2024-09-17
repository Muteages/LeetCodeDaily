# Uncommon Words from Two Sentences

A sentence is a string of single-space separated words where each word consists only of lowercase letters.

A word is uncommon if it appears exactly once in one of the sentences, and does not appear in the other sentence.

Given two sentences s1 and s2, return a list of all the uncommon words. You may return the answer in any order.

## Approach 

Stringstream
``` C++
    vector<string> uncommonFromSentences(string s1, string s2) {
        std::stringstream words(s1 + ' ' + s2);
        std::unordered_map<std::string, int> freq;
        std::string temp{};
        while (words >> temp)
        {
            freq[temp]++;
        }
        std::vector<std::string> ans{};
        for (const auto& [word, f] : freq) 
        {
            if (f == 1)
            {
                ans.emplace_back(std::move(word));
            }
        }
        return ans;
    }
```

String_view

``` C++
    void splitString(std::unordered_map<std::string_view, int>& freq, std::string_view sv)
    {
        int l = 0, r = 0;
        while (r != std::string_view::npos)
        {
            r = sv.find(' ', l);
            freq[sv.substr(l, r - l)]++;
            l = r + 1;
        }
    }
    
    vector<string> uncommonFromSentences(string s1, string s2) {
        std::unordered_map<std::string_view, int> freq;
        splitString(freq, s1);
        splitString(freq, s2);

        std::vector<std::string> ans{};
        for (const auto& [word, f] : freq)
        {
            if (f == 1)
            {
                ans.emplace_back(word);
            }
        }
        return ans;
    }   
```


``` JavaScript
var uncommonFromSentences = function(s1, s2) {
    s1 = s1.split(' ');
    s2 = s2.split(' ');
    const freq = new Map();
    
    const countFrequency = (s) => {
        for (let word of s) {
            if (freq.has(word)) {
                freq.set(word, freq.get(word) + 1);
            }
            else {
                freq.set(word, 1);
            }
        }
    };

    countFrequency(s1);
    countFrequency(s2);
    const ans = new Array();
    for (let [word, f] of freq) {
        if (f === 1) {
            ans.push(word);
        }
    }
    return ans;
};
```
