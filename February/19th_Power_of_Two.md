# Power of Two

https://leetcode.com/problems/power-of-two

Given an integer n, return true if it is a power of two. Otherwise, return false.

## Approach 

Bit manipulation

``` C++
    bool isPowerOfTwo(int n) {
        if (n <= 0)
        {
            return false;
        }
        return n & (n - 1) == 0;
    }
```

## Approach 

Utilise built-in bit check function

``` C++
    bool isPowerOfTwo(int n) {
        if (n <= 0)
        {
            return false;
        }
        int cnt = __builtin_popcount(n);
        // int cnt = std::bitset<31>(n).count();
        return cnt == 1;
    }
```