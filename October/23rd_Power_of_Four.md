# Power of Four

https://leetcode.com/problems/power-of-four

Given an integer n, return true if it is a power of four. Otherwise, return false.

## Approach 1
``` C++
    bool isPowerOfFour(int n) {
        int64_t curr = 1;
        while (curr < n)
        {
            curr *= 4;
        }
        return curr == n;
    }
```

## Approach 2
``` C++
    bool isPowerOfFour(int n) {
        if (n == 0)
        {
            return false;
        }
        while (n % 4 == 0)
        {
            n /= 4;
        }
        return n == 1;
    }
    }
```
## Approach 3

Follow up: solve it without loops/recursion

``` C++
    bool isPowerOfFour(int n) {
        return n > 0 && (n & (n - 1)) == 0 && (n & 0x55555555) == n;
    }
```