# Minimum Deletions to Make Character Frequencies Unique

https://leetcode.com/problems/minimum-deletions-to-make-character-frequencies-unique/description

A string s is called good if there are no two different characters in s that have the same frequency.

Given a string s, return the minimum number of characters you need to delete to make s good.


## Approach 1 

Use unordered_set

``` C++
    int minDeletions(string s) {
        std::unordered_map<char, int> freq; // char - frequency
        for (auto& ch : s)
        {
            freq[ch]++;
        }

        std::unordered_set<int> unique;
        int cnt = 0;
        for (auto [ch, f] : freq)
        {
            while (unique.count(f))
            { // If the current frequency is "occuqied", decrease one time and try again.
                f--;
                cnt++;
            }
            
            if (f > 0)
            {
                unique.insert(f);
            }
        }
        return cnt;
    }
```

## Approach 2

Use priority_queue

``` C++
    int minDeletions(string s) {
        std::unordered_map<char, int> freq;
        for (auto& ch : s)
        {
            freq[ch]++;
        }

        std::priority_queue<int> pq;
        for (auto& [ch, f] : freq)
        {
            pq.emplace(f);
        }

        int cnt = 0;
        while (pq.size() > 1)
        {
            int temp = pq.top();
            pq.pop();
            if (temp == pq.top() && temp != 0)
            {
                temp -= 1;
                cnt++;
                pq.emplace(temp);
            }
        }
        return cnt;
    }
```

