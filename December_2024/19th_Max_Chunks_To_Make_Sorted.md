# Max Chunks To Make Sorted

https://leetcode.com/problems/max-chunks-to-make-sorted

You are given an integer array arr of length n that represents a permutation of the integers in the range [0, n - 1].

We split arr into some number of chunks (i.e., partitions), and individually sort each chunk. After concatenating them, the result should equal the sorted array.

Return the largest number of chunks we can make to sort the array.

## Approach 1

Greedy simulation

``` C++
    int maxChunksToSorted(vector<int>& arr) {
        const int n = arr.size();
        int i = 0, ans = 0;
        while (i < n)
        {
            if (arr[i] == i)
            {
                ans++;
                i++;
                continue;
            }
            if (arr[i] == n - 1)
            { // Make rest of numbers a chunk to make sure the order correct
                ans++;
                break;
            }

            int diff = arr[i]; // Indicates position i - position arr[i] must be at the same chunk in order to make the order correct
            for (int j = i + 1; j <= diff; j++)
            { // Check whether the chunk need to be extended
                diff = std::max(arr[j], diff);
            }
            ans++;
            i = diff + 1; // Move to next possible chunk head
        }
        return ans;
    }
```

## Approach 2

Calculate chunk sum
``` C++
    int maxChunksToSorted(vector<int>& arr) {
        int realSum{}, expectSum{};
        int ans{};
        for (int i = 0; i < arr.size(); i++)
        {
            realSum += arr[i];
            expectSum += i;
            ans += (realSum == expectSum);
        }
        return ans;
    }
```

