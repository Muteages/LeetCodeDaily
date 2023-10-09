# Find First and Last Position of Element in Sorted Array

https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array

Given an array of integers nums sorted in non-decreasing order, find the starting and ending position of a given target value.

If target is not found in the array, return [-1, -1].


## Approach 1
Binary Search

``` C++
    int binarySearch(const std::vector<int>& nums, int target)
    {
        int left = 0;
        int right = nums.size() - 1;
        while (left <= right)
        {
            int mid = left + (right - left) / 2;
            if (nums[mid] < target)
            {
                left = mid + 1;
            }
            else
            {
                right = mid - 1;
            }
        }
        return left;
    }
    vector<int> searchRange(vector<int>& nums, int target) {
        if (nums.empty() || nums.back() < target + 1)
        {
            return {-1, -1};
        }

        int st = binarySearch(nums, target);
        if (st >= nums.size() || nums[st] != target)
        { // Unable to find the target
            return {-1, -1};
        }
        int end = binarySearch(nums, target + 1) - 1;
        return {st, end};
    }
```


## Approach 2
``` C++
    vector<int> searchRange(vector<int>& nums, int target) {
        if (nums.empty() || target > nums.back())
        {
            return {-1, -1};
        }

        auto it = std::find(nums.begin(), nums.end(), target);
        if (it == nums.end())
        {
            return {-1, -1};
        }
        
        int stPos = std::distance(nums.begin(), it);
        int endPos = stPos;
        while (it != nums.end() && *it == target)
        {
            endPos++;
            it++;
        }
        return {stPos, endPos - 1};
    }
```

## Approach 3
``` C++
    vector<int> searchRange(vector<int>& nums, int target) {
        if (nums.empty() || target > nums.back())
        {
            return {-1, -1};
        }

        auto st = std::find(nums.begin(), nums.end(), target);
        if (st == nums.end())
        {
            return {-1, -1};
        }
        auto end = std::find(nums.rbegin(), nums.rend(), target);

        
        int stPos = std::distance(nums.begin(), st);
        int endPos = std::distance(end, nums.rend()) - 1;
        return {stPos, endPos};
    }
```