# Ugly Number II

https://leetcode.com/problems/ugly-number-ii

An ugly number is a positive integer whose prime factors are limited to 2, 3, and 5.

Given an integer n, return the nth ugly number.

## Approach 

``` C++
    int nthUglyNumber(int n) {
        std::vector<int> ugly{1};
        int idx2 = 0, idx3 = 0, idx5 = 0;
        for (int i = 1; i < n; i++)
        {
            int n2 = ugly[idx2] * 2,
                n3 = ugly[idx3] * 3,
                n5 = ugly[idx5] * 5;
            int next = std::min({n2, n3, n5});
            ugly.emplace_back(next);
            if (next == n2) idx2++;
            else if (next == n3) idx3++;
            else if (next == n5) idx5++;
        }
        return ugly.back();
    }
```