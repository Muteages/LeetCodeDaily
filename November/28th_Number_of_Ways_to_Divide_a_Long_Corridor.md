# Number of Ways to Divide a Long Corridor

https://leetcode.com/problems/number-of-ways-to-divide-a-long-corridor

Along a long library corridor, there is a line of seats and decorative plants. You are given a 0-indexed string corridor of length n consisting of letters 'S' and 'P' where each 'S' represents a seat and each 'P' represents a plant.

One room divider has already been installed to the left of index 0, and another to the right of index n - 1. Additional room dividers can be installed. For each position between indices i - 1 and i (1 <= i <= n - 1), at most one divider can be installed.

Divide the corridor into non-overlapping sections, where each section has exactly two seats with any number of plants. There may be multiple ways to perform the division. Two ways are different if there is a position with a room divider installed in the first way but not in the second way.

Return the number of ways to divide the corridor. Since the answer may be very large, return it modulo 109 + 7. If there is no way, return 0.


## Approach 1

``` C++
    int numberOfWays(string corridor) {
        const int mod = 1e9 + 7;
        int total = corridor.length();

        std::vector<int> sofa;
        for (int i = 0; i < total; i++)
        {
            if (corridor[i] == 'S')
            {
                sofa.emplace_back(i);
            }
        }
        int s = sofa.size();
        if (s % 2 != 0 || s == 0)
        { // Unable to make all seactions have 2 seats
            return 0;
        }
        
        int ans = 1;
        for (int i = 1; i < s - 1; i += 2)
        { // Only the gap between adjacent sections need to be considered
            int gap = sofa[i + 1] - sofa[i];
            ans = (ans * (size_t)gap) % mod; 
        }
        return ans;
    }
```

## Approach 2

Improved by removing extra vector
``` C++
    int numberOfWays(string corridor) {
        const int mod = 1e9 + 7;
        int seat = 0;
        int plant = 0;
        int ans = 1;
        for (const char& c : corridor)
        {
            if (c == 'S')
            {
                seat++;
            }
            else
            {
                if (seat == 2)
                {
                    plant++;
                }
            }

            if (seat == 3)
            { // Find another section
                ans = (ans * (size_t)(plant + 1)) % mod;
                seat = 1;
                plant = 0;
            }
        }

        if (seat != 2)
        { // Unable to divide the last section as required
            return 0;
        }
        return ans;
    }
```