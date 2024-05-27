# Special Array With X Elements Greater Than or Equal X

https://leetcode.com/problems/special-array-with-x-elements-greater-than-or-equal-x

You are given an array nums of non-negative integers. nums is considered special if there exists a number x such that there are exactly x numbers in nums that are greater than or equal to x.

Notice that x does not have to be an element in nums.

Return x if the array is special, otherwise, return -1. It can be proven that if nums is special, the value for x is unique.

## Approach 1

``` C++
    int specialArray(vector<int>& nums) {
        std::sort(nums.begin(), nums.end());
        int n = nums.size();
        for (int special = 0, i = 0; i < n; special++)
        {
            while (i < n && nums[i] < special)
            {
                i++;
            }
            if (n - i == special)
            {
                return special;
            }
        }
        return -1;
    }
```
## Approach 2

Counting sort
``` C++
    int specialArray(vector<int>& nums) {
        std::vector<int> freq(1001, 0);
        for (int num : nums)
        {
            freq[num]++;
        }
        int greater = nums.size();
        for (int i = 0; i < 101; i++)
        {
            if (greater == i)
            {
                return i;
            }
            greater -= freq[i];
        }
        return -1;
    }
```