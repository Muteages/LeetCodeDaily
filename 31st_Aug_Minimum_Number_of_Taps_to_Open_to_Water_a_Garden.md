# Minimum Number of Taps to Open to Water a Garden

https://leetcode.com/problems/minimum-number-of-taps-to-open-to-water-a-garden/description/

There is a one-dimensional garden on the x-axis. The garden starts at the point 0 and ends at the point n. (i.e The length of the garden is n).

There are n + 1 taps located at points [0, 1, ..., n] in the garden.

Given an integer n and an integer array ranges of length n + 1 where ranges[i] (0-indexed) means the i-th tap can water the area [i - ranges[i], i + ranges[i]] if it was open.

Return the minimum number of taps that should be open to water the whole garden, If the garden cannot be watered return -1.


## Approach 1

``` C++
    int minTaps(int n, vector<int>& ranges) {
        std::vector<std::pair<int, int>> pairs(n + 1); // left - right range positions

        for (int i = 0; i <= n; i++)
        { // Initialise the pairs
            pairs[i] = {i - ranges[i], i + ranges[i]};
        }

        std::sort(pairs.begin(), pairs.end());

        int prevRight = INT_MIN;
        int curTap = 0;
        while (curTap <= n && pairs[curTap].first <= 0)
        { // Find the first tap which covers the left side while having the farthest right side
            prevRight = std::max(pairs[curTap].second, prevRight);
            curTap++;
        }

        int taps = 1;
        if (prevRight >= n)
        { // Garden is covered already.
            return taps;
        }

        while (prevRight < n)
        {
            int curRight = prevRight;
            while (curTap <= n && pairs[curTap].first <= prevRight)
            { // Find the new farthest right
                curRight = std::max(pairs[curTap].second, curRight);
                curTap++;
            }

            if (curRight == prevRight)
            { // Have a gap, fail
                return -1;
            }

            taps++;
            prevRight = curRight;
        }

        return taps;   
    }
```


## Approach 2 (Slower but.. cleaner?)

``` C++
    int minTaps(int n, vector<int>& ranges) {
        int left = 0;
        int right = 0;
        int taps = 0;
        while (right < n)
        {
            for (int i = 0; i <= n; i++)
            {
                if (i - ranges[i] <= left && i + ranges[i] >= right)
                { // Check if the current tap is able to cover the current range
                    right = i + ranges[i];
                }
            }

            if (left == right)
            { // Indicates there is a gap, i.e we can't go further
                return -1;
            }

            taps++;
            left = right; // Update the range
        }

        return taps;
    }
```

## Approach 3

``` C++
    int minTaps(int n, vector<int>& ranges) {
        std::vector<int> reachable(n + 1);

        for (int i = 0; i <= n; i++)
        {
            if (ranges[i] != 0)
            { // Update the farthest position that one tap can reach
                int left = std::max(0, i - ranges[i]);
                reachable[left] = std::max(reachable[left], i + ranges[i]);
            }
        }

        int curRight = 0;
        int farthestPoint = 0;
        int taps = 0;
        int curTap = 0;
        while (curRight < n)
        {
            while (curTap <= curRight)
            {
                farthestPoint = std::max(farthestPoint, reachable[curTap]);
                curTap++;
            }

            if (farthestPoint <= curRight)
            { // Unable to cover the garden
                return -1;
            }

            curRight = farthestPoint;
            taps++;
        }

        return taps;
    }
```