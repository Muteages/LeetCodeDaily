# Number of 1 Bits

https://leetcode.com/problems/number-of-1-bits/description

Write a function that takes the binary representation of an unsigned integer and returns the number of '1' bits it has.


## Approach 1
Built in function | bitset
``` C++
    int hammingWeight(uint32_t n) {
        return __builtin_popcount(n);
        //return std::bitset<32>(n).count();
    }
```

## Approach 2
``` C++
    int hammingWeight(uint32_t n) {
        int ans = 0;
        while (n > 0)
        {
            ans++;
            n &= (n - 1);
        }
        return ans;
    }
```

