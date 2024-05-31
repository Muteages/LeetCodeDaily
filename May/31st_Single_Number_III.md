# Single Number III

https://leetcode.com/problems/single-number-iii



Given an integer array nums, in which exactly two elements appear only once and all the other elements appear exactly twice. Find the two elements that appear only once. You can return the answer in any order.

You must write an algorithm that runs in linear runtime complexity and uses only constant extra space.


## Approach 

``` C++
    vector<int> singleNumber(vector<int>& nums) {
        int xorSum = 0;
        for (int num : nums)
        {
            xorSum ^= num;
        }

        // Find a '1' digit, which indicates that two target numbers are different at current digit
        int digit = 31;
        while (((xorSum >> digit) & 1) == 0)
        {
            digit--;
        }
        int xor0 = 0, xor1 = 0; // Divide two numbers
        for (int num : nums)
        {
            if (((num >> digit) & 1) == 0)
            {
                xor0 ^= num;
            }
            else
            {
                xor1 ^= num;
            }
        }
        return {xor0, xor1};
    }
```