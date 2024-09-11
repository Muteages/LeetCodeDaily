# Minimum Bit Flips to Convert Number

A bit flip of a number x is choosing a bit in the binary representation of x and flipping it from either 0 to 1 or 1 to 0.

## Approach 1

``` C++
    int minBitFlips(int start, int goal) {
        int XOR = start ^ goal;
        std::bitset<32> bits(XOR);
        return bits.count();
    }
```

## Approach 2

``` C++
    int minBitFlips(int x, int y) {
        int ans = 0;
        while (x > 0 || y > 0)
        {
            ans += ((x & 1) ^ (y & 1));
            x >>= 1;
            y >>= 1;
        }
        return ans;
    }
```
