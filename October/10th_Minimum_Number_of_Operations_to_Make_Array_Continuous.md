# Minimum Number of Operations to Make Array Continuous

https://leetcode.com/problems/minimum-number-of-operations-to-make-array-continuous

You are given an integer array nums. In one operation, you can replace any element in nums with any integer.

nums is considered continuous if both of the following conditions are fulfilled:

All elements in nums are unique.
The difference between the maximum element and the minimum element in nums equals nums.length - 1.
For example, nums = [4, 2, 5, 3] is continuous, but nums = [1, 2, 3, 5, 6] is not continuous.

Return the minimum number of operations to make nums continuous.

## Approach 1

Sliding window
``` C++
    int minOperations(vector<int>& nums) {
        if (nums.size() == 1)
        {
            return 0;
        }
        int n = nums.size();
        std::sort(nums.begin(), nums.end());
        auto it = std::unique(nums.begin(), nums.end());
        nums.erase(it, nums.end()); // Remove duplicates

        int minCost = INT_MAX;
        int right = 0;
        for (int left = 0; left < nums.size(); left++)
        {
            while (right < nums.size() && nums[right] < nums[left] + n)
            { // Find the first element which is greater than target right boundary
                right++;
            }

            minCost = std::min(minCost, n - (right - left));
        }

        return minCost;
    }
```

## Approach 2

Binary search
``` C++

    /*   Equals to std::upper_bound func
    int binarySearch(vector<int>& nums, int l, int r, int target)
    {
        while (l <= r)
        {
            int mid = l + (r - l) * 0.5;
            if (nums[mid] < target)
            {
                l = mid + 1;
            }
            else
            {
                r = mid - 1;
            }

        }
        return l;
    }
    */

    int minOperations(vector<int>& nums) {
        if (nums.size() == 1)
        {
            return 0;
        }
        int n = nums.size();
        std::sort(nums.begin(), nums.end());
        auto it = std::unique(nums.begin(), nums.end());
        nums.erase(it, nums.end()); // Remove duplicates

        int minCost = INT_MAX;
        for (int i = 0; i < nums.size(); i++)
        {
            int left = nums[i];
            int right = n - 1 + left;
            int rightPos = std::upper_bound(nums.begin(), nums.end(), right) - nums.begin();
            // int rightPos = binarySearch(nums, i, nums.size() - 1, right + 1);
            minCost = std::min(minCost, n - (rightPos - i));
        }

        return minCost;
    }
```


