# Hand of Straights

https://leetcode.com/problems/hand-of-straights

Alice has some number of cards and she wants to rearrange the cards into groups so that each group is of size groupSize, and consists of groupSize consecutive cards.

Given an integer array hand where hand[i] is the value written on the ith card and an integer groupSize, return true if she can rearrange the cards, or false otherwise.

## Approach 


``` C++
    bool isNStraightHand(vector<int>& hand, int groupSize) {
        int n = hand.size();
        if (n % groupSize != 0)
        {
            return false;
        }

        std::map<int, int> freq;
        for (int num : hand)
        {
            freq[num]++;
        }

        while (!freq.empty())
        {
            auto st = freq.begin();
            auto ed = std::next(freq.begin(), groupSize - 1);
            if (ed->first - st->first != groupSize - 1 || ed == freq.end())
            {
                return false;
            }
            for (int i = 0; i < groupSize; ++i)
            {
                st->second--;
                if (st->second == 0)
                {
                    st = freq.erase(st);
                }                
                else
                {
                    st++;
                }
            }
        }
        return true;
    }
```

## Approach 2

Without deleting the elements from the map.  Greedy

``` C++
    bool isNStraightHand(vector<int>& hand, int groupSize) {
        int n = hand.size();
        if (n % groupSize != 0)
        {
            return false;
        }

        std::map<int, int> freq;
        for (int num : hand)
        {
            freq[num]++;
        }

        for (auto [num, f] : freq)
        {
            if (f == 0)
            {
                continue;
            }
            for (int i = num; i < num + groupSize; ++i)
            {
                if (!freq.count(i) || freq[i] < f)
                {   
                    return false;
                }
                freq[i] -= f;
            }
        }
        return true;
    }
```


``` JavaScript

// Map
var isNStraightHand = function(hand, groupSize) {
    let n = hand.length;
    if (n % groupSize !== 0) {
        return false;
    }

    hand.sort((a, b) => a - b);
    let freq = new Map();
    for (let num of hand) {
        freq.set(num, (freq.get(num) || 0) + 1);
    }

    for (let [num, f] of freq) {
        if (f === 0) {
            continue;
        }
        for (let i = num; i < num + groupSize; i++)
        {
            if (!freq.has(i) || freq.get(i) < f) {
                return false;
            }
            freq.set(i, freq.get(i) - f);
        }
    }
    return true;
};

// Object
var isNStraightHand = function(hand, groupSize) {
    let n = hand.length;
    if (n % groupSize !== 0) {
        return false;
    }
    hand.sort((a, b) => a - b);
    let freq = {};
    for (let num of hand)
    {
        freq[num] = (freq[num] || 0) + 1;
    }

    for (let ns in freq)
    {
        let num = +ns;
        let f = freq[num];
        if (f === 0)
        {
            continue;
        }

        for (let i = num; i < num + groupSize; i++)
        {
            if (freq[i] === undefined || freq[i] < f)
            {
                return false;
            }
            freq[i] -= f;
        }
    }
    return true;
};
```