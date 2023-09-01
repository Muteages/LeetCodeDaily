# Counting Bits

https://leetcode.com/problems/counting-bits/description/

Given an integer n, return an array ans of length n + 1 such that for each i (0 <= i <= n), ans[i] is the number of 1's in the binary representation of i.


## Approach

``` C++
    vector<int> countBits(int n) {
        std::vector<int> ans(n + 1, 0);

        for (int i = 0; i <= n; i++)
        {
            // ans[i] = ans[i / 2] + i % 2;
            ans[i] = ans[i >> 1] + (i & 1);
        }

        return ans;
    }
```