# Number Complement

https://leetcode.com/problems/number-complement

The complement of an integer is the integer you get when you flip all the 0's to 1's and all the 1's to 0's in its binary representation.

For example, The integer 5 is "101" in binary and its complement is "010" which is the integer 2.
Given an integer num, return its complement.

 
## Approach 1

``` C++
    int findComplement(int num) {
        if (num == 1) return 0;
        int digit = 0, ans = 0;
        while (num > 0)
        {
            ans += (1 - (num & 1)) << digit;
            digit++;
            num >>= 1;
        }
        return ans;
    }
```

## Approach 2

``` C++
    int findComplement(int num) {
        if (num == 1) return 0;
        int digit = 0;
        while (std::pow(2, digit) <= num)
        {
            digit++;
        }
        int ans = 0;
        for (int i = 0; i < digit; i++)
        {
            if (((1 << i) & num) == 0)
            {
                ans += std::pow(2, i);
            }
        }
        return ans;
    }
```