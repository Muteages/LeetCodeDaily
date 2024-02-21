# Bitwise AND of Numbers Range

https://leetcode.com/problems/bitwise-and-of-numbers-range

Given two integers left and right that represent the range [left, right], return the bitwise AND of all numbers in this range, inclusive.


## Approach 1

x & (x - 1) means remove the rightmost 1 digit
``` C++
    int rangeBitwiseAnd(int left, int right) {
        if (left == right || left == 0)
        {
            return left;
        }

        while (right > left)
        {
            right &= right - 1;
        }
        return right;
    }
```


## Approach 2

``` C++
    int rangeBitwiseAnd(int left, int right) {
        if (left == right || left == 0)
        {
            return left;
        }

        // Find first number above left boundary
        int aboveLeft = std::ceil(std::log2(left));
        if (std::pow(2, aboveLeft) == left)
        {
            aboveLeft += 1;
        }
        if (std::pow(2, aboveLeft) <= right)
        {
            return 0;
        }

        int ans = right;
        for (int i = left; i < right; i++)
        {
            ans &= i;
        }
        return ans;
    }
```
