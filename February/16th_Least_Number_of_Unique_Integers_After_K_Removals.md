# Least Number of Unique Integers After K Removals

https://leetcode.com/problems/least-number-of-unique-integers-after-k-removals

Given an array of integers arr and an integer k. Find the least number of unique integers after removing exactly k elements.

## Approach 

``` C++
    int findLeastNumOfUniqueInts(vector<int>& arr, int k) {
        std::unordered_map<int, int> freq;
        for (const int& num : arr)
        {
            freq[num]++;
        }

        std::priority_queue<int, std::vector<int>, std::greater<int>> pq;
        for (const auto& [num, f] : freq)
        {
            pq.emplace(f);
        }

        while (k)
        {
            if (k >= pq.top())
            {
                k -= pq.top();
                pq.pop();
            }
            else
            { // Fails to remove current element, break the loop  
                break;
            }
        }
        return pq.size();
    }
```