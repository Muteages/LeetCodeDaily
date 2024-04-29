# Minimum Number of Operations to Make Array XOR Equal to K

https://leetcode.com/problems/minimum-number-of-operations-to-make-array-xor-equal-to-k/

You are given a 0-indexed integer array nums and a positive integer k.

You can apply the following operation on the array any number of times:

Choose any element of the array and flip a bit in its binary representation. Flipping a bit means changing a 0 to 1 or vice versa.
Return the minimum number of operations required to make the bitwise XOR of all elements of the final array equal to k.

## Approach 1

Use bitset 

``` C++
    int minOperations(vector<int>& nums, int k) {
        std::bitset<20> xorSum(k);
        for (int num : nums)
        {
            xorSum ^= num;
        }
        return xorSum.count();
    }
```

## Approach 2

Count 1's count one digit by one digit.
``` C++
    int minOperations(vector<int>& nums, int k) {
        for (int num : nums)
        {
            k ^= num;
        }
        int operations = 0;
        while (k > 0)
        {
            k = (k & (k - 1));
            operations++;
        }
        return operations;
    }
```