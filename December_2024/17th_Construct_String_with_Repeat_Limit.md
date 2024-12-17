# Construct String with Repeat Limit

https://leetcode.com/problems/construct-string-with-repeat-limit

You are given a string s and an integer repeatLimit. Construct a new string repeatLimitedString using the characters of s such that no letter appears more than repeatLimit times in a row. You do not have to use all characters from s.

Return the lexicographically largest repeatLimitedString possible.

A string a is lexicographically larger than a string b if in the first position where a and b differ, string a has a letter that appears later in the alphabet than the corresponding letter in b. If the first min(a.length, b.length) characters do not differ, then the longer string is the lexicographically larger one.


## Approach 1

Priority_Queue
``` C++
    string repeatLimitedString(string s, int repeatLimit) {
        std::vector<int> freq(26, 0);
        for (const char ch : s)
        {
            freq[ch - 'a']++;
        }

        std::priority_queue<std::pair<char, int>> pq;
        for (int i = 25; i >= 0; i--)
        {
            if (freq[i] != 0)
            {
                pq.emplace(i + 'a', freq[i]);
            }
        }

        std::string ans{};
        while (!pq.empty())
        {
            auto [letter, f] = pq.top();
            pq.pop();
            if (f <= repeatLimit)
            {
                ans += std::string(f, letter);
            }
            else
            {
                ans += std::string(repeatLimit, letter);
                if (pq.empty()) break;
                auto [lNext, fNext] = pq.top();
                pq.pop();
                ans += std::string(1, lNext);
                if (--fNext > 0)
                {
                    pq.emplace(lNext, fNext);
                }
                pq.emplace(letter, f - repeatLimit);
            }
        }
        return ans;
    }
```

## Approach 2

``` C++
   string repeatLimitedString(string s, int repeatLimit) {
        std::vector<int> freq(26, 0);
        for (const char ch : s)
        {
            freq[ch - 'a']++;
        }

        int current{25};
        while (freq[current] == 0)
        {
            current--;
        }
        int next{current - 1};
        std::string ans{};

        while (next >= 0)
        {
            // Check if the current letter is avaliable
            if (freq[current] > repeatLimit)
            { // Case 1: have more than limit counts, use limited number and fill a second largest letter
                ans += std::string(repeatLimit, current + 'a');
                freq[current] -= repeatLimit;
                while (next >= 0 && freq[next] == 0)
                {
                    next--;
                }
                if (next < 0) break;
                ans += std::string(1, next + 'a');
                freq[next]--;
            }
            else if (freq[current] > 0)
            { // Case 2: The number of remaining letter less than the limit, reuse all and move to next avaliable position
                ans += std::string(freq[current], current + 'a');
                current = next;
                while (current > 0 && freq[current] == 0)
                {
                    current--;
                }
                next = current - 1;
            }
            else
            {
                current--;
                next--;
            }
        }
        if (ans.empty() || ans.back() != current + 'a')
        {
            ans += std::string(std::min(repeatLimit, freq[current]), current + 'a');
        }
        return ans;
    }
```

Improved
``` C++
    string repeatLimitedString(string s, int repeatLimit) {
        std::vector<int> freq(26, 0);
        for (const char ch : s)
        {
            freq[ch - 'a']++;
        }

        int current{25}, next{24};
        std::string ans{};
        while (current >= 0)
        {
            while (current > 0 && freq[current] == 0)
            {
                current--;
            }
            int repeat = std::min(freq[current], repeatLimit);
            ans += std::string(repeat, current + 'a');
            freq[current] -= repeat;
            
            if (freq[current] > 0)
            { // Indicates the largest letter still exist
                while (next >= 0 && (freq[next] == 0 || next >= current)) 
                {
                    next--;
                }

                if (next < 0) break;
                ans += std::string(1, next + 'a');
                freq[next]--;
            }
            else
            {
                current--;
            }
        }
        return ans;
    }
```

## Approach 3

``` JavaScript
var repeatLimitedString = function(s, repeatLimit) {
    const freq = new Array(26).fill(0);
    for (const ch of s) {
        freq[ch.charCodeAt(0) - 'a'.charCodeAt(0)]++;
    }

    let current = 25, next = 24; // Start from the largest letter
    let ans = [];
    while (current >= 0) {
        while (freq[current] === 0) {
            current--;
        }
        let repeat = Math.min(freq[current], repeatLimit);
        ans.push(String.fromCharCode(97 + current).repeat(repeat));
        freq[current] -= repeat;
        if (freq[current] > 0) {
            while (next >= 0 && (freq[next] === 0 || next >= current)) {
                next--;
            }
            if (next < 0) break;
            ans.push(String.fromCharCode(97 + next));
            freq[next]--;
        }
        else {
            current--;
        }
    }
    return ans.join('');
};
```

