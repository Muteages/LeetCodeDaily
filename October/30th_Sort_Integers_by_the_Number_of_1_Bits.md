# Sort Integers by the Number of 1 Bits

https://leetcode.com/problems/sort-integers-by-the-number-of-1-bits

You are given an integer array arr. Sort the integers in the array in ascending order by the number of 1's in their binary representation and in case of two or more integers have the same number of 1's you have to sort them in ascending order.

Return the array after sorting it.

## Approach 1

Built in function
``` C++
    vector<int> sortByBits(vector<int>& arr) {
        std::sort(arr.begin(), arr.end(), [](int l, int r){
            int bitL = __builtin_popcount(l);
            int bitR = __builtin_popcount(r);
            if (bitL == bitR)
            {
                return l < r;
            }
            else
            {
                return bitL < bitR;
            }
            });

        return arr;
    }
```

## Approach 2

``` C++
    int countBit(int n)
    {
        int cnt = 0;
        while (n > 0)
        {
            cnt++;
            n &= (n - 1);
        }
        return cnt;
    }
    vector<int> sortByBits(vector<int>& arr) {
        std::sort(arr.begin(), arr.end(), 
        [&](int l, int r){
            int bitL = countBit(l);
            int bitR = countBit(r);
            if (bitL == bitR)
            {
                return l < r;
            }
            else
            {
                return bitL < bitR;
            }
            });

        return arr;
    }
```