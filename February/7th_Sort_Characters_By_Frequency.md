# Sort Characters By Frequency

https://leetcode.com/problems/sort-characters-by-frequency

Given a string s, sort it in decreasing order based on the frequency of the characters. The frequency of a character is the number of times it appears in the string.

Return the sorted string. If there are multiple answers, return any of them.

## Approach 1

Brute force by using hash map && sorting 
``` C++
    string frequencySort(string s) {
        std::unordered_map<char, int> freq;
        for (const auto& ch : s)
        {
            freq[ch]++;
        }

        std::vector<std::pair<int, char>> sorted;
        for(const auto& [ch, f] : freq)
        {
            sorted.emplace_back(f, ch);
        }

        std::sort(sorted.begin(), sorted.end(), [](const std::pair<int, char>& l, const std::pair<int, char>& r){
            return l.first > r.first;
        });

        std::string ans{};
        for (const auto& [f, ch] : sorted)
        {
            ans += std::string(f, ch);
        }
        return ans;
    }
```

## Approach 2

Utilise pripority_queue

``` C++
    string frequencySort(string s) {
        std::unordered_map<char, int> freq;
        for (const auto& ch : s)
        {
            freq[ch]++;
        }

        std::priority_queue<std::pair<int, char>> pq;
        for (const auto& [ch, f] : freq)
        {
            pq.emplace(f, ch);
        }

        std::string ans{};
        while (!pq.empty())
        {
            auto [f, ch] = pq.top();
            pq.pop();
            ans += std::string(f, ch);
        }
        return ans;
    }
```

