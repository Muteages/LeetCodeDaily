# Find All Duplicates in an Array

https://leetcode.com/problems/find-all-duplicates-in-an-array/

Given an integer array nums of length n where all the integers of nums are in the range [1, n] and each integer appears once or twice, return an array of all the integers that appears twice.

You must write an algorithm that runs in O(n) time and uses only constant extra space.

## Approach 

``` C++
    vector<int> findDuplicates(vector<int>& nums) {
        std::vector<int> duplicates;
        for (int num : nums)
        {
            num = std::abs(num);
            if (nums[num - 1] < 0)
            { // Indicates nums[num - 1] was visited before, i.e num is a duplicate
                duplicates.emplace_back(num);
            }
            else
            {
                nums[num - 1] *= -1;
            }
        }        
        return duplicates;
    }
```