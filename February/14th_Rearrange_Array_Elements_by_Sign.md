# Rearrange Array Elements by Sign

https://leetcode.com/problems/rearrange-array-elements-by-sign

You are given a 0-indexed integer array nums of even length consisting of an equal number of positive and negative integers.

You should rearrange the elements of nums such that the modified array follows the given conditions:

Every consecutive pair of integers have opposite signs.
For all integers with the same sign, the order in which they were present in nums is preserved.
The rearranged array begins with a positive integer.
Return the modified array after rearranging the elements to satisfy the aforementioned conditions.

## Approach 1

``` C++
    vector<int> rearrangeArray(vector<int>& nums) {
        int n = nums.size();
        std::vector<int> ans(n);
        int positive = 0, negative = 1;
        for (int i = 0; i < n; i++)
        {
            if (nums[i] > 0)
            {
                ans[positive] = nums[i];
                positive += 2;
            }
            else
            {
                ans[negative] = nums[i];
                negative += 2;
            }
        }
        return ans;
    }
```

## Approach 2

Rearrange the array in-place

``` C++
    vector<int> rearrangeArray(vector<int>& nums) {
        bool positive = true;
        for (int i = 0; i < nums.size(); i++)
        {
            int next = i + 1;
            if (positive)
            {
                while (nums[i] < 0)
                {
                    std::swap(nums[i], nums[next++]);
                }
                positive = false;
            }
            else
            {
                while (nums[i] > 0)
                {
                    std::swap(nums[i], nums[next++]);
                }
                positive = true;
            }
        }
        return nums;
    }
```