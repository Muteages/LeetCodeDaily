# Number of Flowers in Full Bloom

https://leetcode.com/problems/number-of-flowers-in-full-bloom

You are given a 0-indexed 2D integer array flowers, where flowers[i] = [starti, endi] means the ith flower will be in full bloom from starti to endi (inclusive). You are also given a 0-indexed integer array people of size n, where people[i] is the time that the ith person will arrive to see the flowers.

Return an integer array answer of size n, where answer[i] is the number of flowers that are in full bloom when the ith person arrives.


## Approach 1

MLE for big test case
``` C++
    vector<int> fullBloomFlowers(vector<vector<int>>& flowers, vector<int>& people) {
        std::unordered_map<int, int> bloom; // time - bloom flowers count
        for (auto& flower : flowers)
        {
            int st = flower[0];
            int end = flower[1];
            for (;st <= end; st++)
            {
                bloom[st]++;
            }
        }

        std::vector<int> ans;
        for (int& p : people)
        {
            ans.emplace_back(bloom[p]);
        }
        return ans;
    }
```

## Approach 2

Improve the first approch by using Prefix to avoid a double for loop
``` C++
    vector<int> fullBloomFlowers(vector<vector<int>>& flowers, vector<int>& people) {
        std::map<int, int> bloom; // time - bloom flowers count

        for (auto& p : people)
        {
            bloom[p] = 0;
        }
        for (auto& flower : flowers)
        { // Prefix
            int st = flower[0];
            int end = flower[1];
            bloom[st]++;
            bloom[end + 1]--; // The first time that out of range will lose one flower cnt
        }

        int prevBloom = 0;
        for (auto& [t, cnt] : bloom)
        { // Update the bloom counts
            cnt += prevBloom;
            prevBloom = cnt;
        }

        std::vector<int> ans;
        for (int& p : people)
        {
            ans.emplace_back(bloom[p]);
        }
        return ans;
    }
```