# Monotonic Array

https://leetcode.com/problems/monotonic-array

An array is monotonic if it is either monotone increasing or monotone decreasing.

An array nums is monotone increasing if for all i <= j, nums[i] <= nums[j]. An array nums is monotone decreasing if for all i <= j, nums[i] >= nums[j].

Given an integer array nums, return true if the given array is monotonic, or false otherwise.


## Approach 1
``` C++
    bool isMonotonic(vector<int>& nums) {
        auto increasing = nums;
        std::sort(increasing.begin(), increasing.end());
        auto decreasing = nums;
        std::sort(decreasing.begin(), decreasing.end(), std::greater<int>());

        return nums == increasing || nums == decreasing;
    }
```

## Approach 2
``` C++
    bool isMonotonic(vector<int>& nums) {

        int flag = 0; // 0 - unknown, 1 - increase, -1 = decrease

        for (int i = 1; i < nums.size(); i++)
        {
            if (nums[i] < nums[i - 1])
            {
                if (flag == 0)
                {
                    flag = -1;
                }
                else if (flag == 1)
                {
                    return false;
                }
            }
            else if (nums[i] > nums[i - 1])
            {
                if (flag == 0)
                {
                    flag = 1;
                }
                else if (flag == -1)
                {
                    return false;
                }
            }
        }
        return true;
    }
```