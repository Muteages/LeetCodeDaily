# Sum of All Subset XOR Totals

https://leetcode.com/problems/sum-of-all-subset-xor-totals

The XOR total of an array is defined as the bitwise XOR of all its elements, or 0 if the array is empty.

For example, the XOR total of the array [2,5,6] is 2 XOR 5 XOR 6 = 1.
Given an array nums, return the sum of all XOR totals for every subset of nums. 

Note: Subsets with the same elements should be counted multiple times.

An array a is a subset of an array b if a can be obtained from b by deleting some (possibly zero) elements of b.

## Approach 
Backtracking
``` C++
    int acc(std::vector<int>& nums, int idx, int sum)
    {
        if (idx == nums.size())
        {
            return sum;
        }

        int take = acc(nums, idx + 1, sum ^ nums[idx]); // Include the current element
        int skip = acc(nums, idx + 1, sum);         // Skip the current element
        return take + skip;
    }

    int subsetXORSum(vector<int>& nums) {
        return acc(nums, 0, 0);
    }
```
