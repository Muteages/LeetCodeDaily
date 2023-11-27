# Knight Diagler

The chess knight has a unique movement, it may move two squares vertically and one square horizontally, or two squares horizontally and one square vertically (with both forming the shape of an L).
Given an integer n, return how many distinct phone numbers of length n we can dial.

You are allowed to place the knight on any numeric cell initially and then you should perform n - 1 jumps to dial a number of length n. All jumps should be valid knight jumps.

As the answer may be very large, return the answer modulo 109 + 7.

## Approach 

DP
``` C++
    int knightDialer(int n) {
        const int mod = 1e9 + 7;
        std::vector<size_t> prev(10, 1);
        std::vector<size_t> curr(10, 0);
        for (int i = 2; i <= n; i++)
        {
            curr[0] = (prev[4] + prev[6]) % mod;
            curr[1] = (prev[6] + prev[8]) % mod;
            curr[2] = (prev[7] + prev[9]) % mod;
            curr[3] = (prev[4] + prev[8]) % mod;
            curr[4] = (prev[0] + prev[3] + prev[9]) % mod;
            curr[6] = (prev[0] + prev[1] + prev[7]) % mod;
            curr[7] = (prev[2] + prev[6]) % mod;
            curr[8] = (prev[1] + prev[3]) % mod;
            curr[9] = (prev[2] + prev[4]) % mod;
            prev = curr;
        }

        int ans = 0;
        for (int i = 0; i < 10; i++)
        {
            ans = (ans + prev[i]) % mod;
        } 
        return ans;
    }
```

