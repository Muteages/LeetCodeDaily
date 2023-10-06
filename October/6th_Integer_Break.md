# Integer Break

https://leetcode.com/problems/integer-break

Given an integer n, break it into the sum of k positive integers, where k >= 2, and maximize the product of those integers.

Return the maximum product you can get.

## Approach 1

``` C++
    int integerBreak(int n) {
        // No more than one 4 and two 2, because 4 * 4 < 3 * 3 * 2,   2 * 2 * 2 < 3 * 3 
        if (n <= 3)
        {
            return n - 1;
        }

        int nums = n / 3;
        int rem = n % 3;

        if (rem == 0)
        {
            return std::pow(3, nums);
        }
        else if (rem == 1)
        {
            return std::pow(3, nums - 1) * 4;
        }
        else
        {
            return std::pow(3, nums) * rem;
        }
    }
```

## Approach 2
``` C++
    int integerBreak(int n) {
        // No more than one 4 and two 2, because 4 * 4 < 3 * 3 * 2,   2 * 2 * 2 < 3 * 3 
        if (n <= 3)
        {
            return n - 1;
        }

        int ans = 1;
        while (n > 4)
        { // To make sure every time the remainder is greater than 1.
            ans *= 3;
            n -= 3;
        }

        ans *= n;
        return ans;
    }
```