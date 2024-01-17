# Unique Number of Occurrences

https://leetcode.com/problems/unique-number-of-occurrences

Given an array of integers arr, return true if the number of occurrences of each value in the array is unique or false otherwise.


## Approach 1

hash map and hash set 

``` C++
    bool uniqueOccurrences(vector<int>& arr) {
        std::unordered_map<int, int> ump;
        for (int i : arr)
        {
            ump[i]++;
        }
        std::unordered_set<int> cnt;
        for (auto [val, count] : ump)
        {
            if (cnt.count(count))
            {
                return false;
            }
            cnt.insert(count);
        }
        return true;
    }
```

## Approach 2
constant SC
``` C++
    bool uniqueOccurrences(vector<int>& arr) {
        std::vector<int> occurrences(2001, 0);
        for (const int& num : arr)
        {
            occurrences[num + 1000]++;
        }

        std::vector<int> unique(1001, 0);
        for (const int& occurrence : occurrences)
        {
            if (occurrence > 0 && unique[occurrence] == 1)
            { 
                return false;
            }
            unique[occurrence] = 1;
        }
        return true;
    }
```

## Approach 3

``` C++
    bool uniqueOccurrences(vector<int>& arr) {
        std::vector<int> occurrences(2001, 0);
        for (const int& num : arr)
        {
            occurrences[num + 1000]++;
        }

        std::sort(occurrences.begin(), occurrences.end());
        int i = 0;
        while (occurrences[i] == 0)
        { // Skip 0 occurrences
            i++;
        }
        while (i < 2000)
        {
            if (occurrences[i] == occurrences[i + 1])
            {
                return false;
            }
            i++;
        }
        return true;
    }
```