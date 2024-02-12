# Majority Element

https://leetcode.com/problems/majority-element

Given an array nums of size n, return the majority element.

The majority element is the element that appears more than ⌊n / 2⌋ times. You may assume that the majority element always exists in the array.

## Approach 1

``` C++
    int majorityElement(vector<int>& nums) {
        std::sort(nums.begin(), nums.end());
        return nums[nums.size() / 2];
    }
```

## Approach 2

Boyer-Moore majority vote algorithm

``` C++
    int majorityElement(vector<int>& nums) {
        int n = nums.size();
        int majority = 0;
        int cnt = 0;
        for (const auto& num : nums)
        {
            if (cnt == 0)
            {
                majority = num;
            }
            cnt += (majority == num) ? 1 : -1;
        }
        return majority;
    }
```


