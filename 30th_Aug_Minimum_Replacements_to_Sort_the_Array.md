# Minimum Replacements to Sort the Array

https://leetcode.com/problems/minimum-replacements-to-sort-the-array/description/

You are given a 0-indexed integer array nums. In one operation you can replace any element of the array with any two elements that sum to it.

For example, consider nums = [5,6,7]. In one operation, we can replace nums[1] with 2 and 4 and convert nums to [5,2,4,7]. __(Bad Example)__
Return the minimum number of operations to make an array that is sorted in non-decreasing order.

## Approach 

``` C++
    long long minimumReplacement(vector<int>& nums) {
        if (nums.size() == 1)
        {
            return 0;
        }

        long long count = 0;
        int dummyLast = nums.back(); // Keep tracking the "last" number. i.e the next number of the current element

        for (int i = nums.size() - 2; i >= 0; i--)
        {
            if (nums[i] > dummyLast)
            {
                int steps = (nums[i] - 1) / dummyLast;
                dummyLast = nums[i] / (steps + 1);
                count += (long long)steps;
            }
            else 
            {
                dummyLast = nums[i];
            }
        }
        return count;
    }
```