# Count Subarrays with Fixed Bounds

https://leetcode.com/problems/count-subarrays-with-fixed-bounds

You are given an integer array nums and two integers minK and maxK.

A fixed-bound subarray of nums is a subarray that satisfies the following conditions:

The minimum value in the subarray is equal to minK.
The maximum value in the subarray is equal to maxK.
Return the number of fixed-bound subarrays.

## Approach
``` C++
    long long countSubarrays(vector<int>& nums, int minK, int maxK) {
        long long cnt = 0;
        int curMin = -1, curMax = -1;
        for (int left = 0, int right = 0; right < nums.size(); right++)
        {
            int num = nums[right];
            if (num < minK || num > maxK)
            { // Out of boundary
                left = right + 1;
            }
            if (num == minK)
            {
                curMin = right;
            }
            if (num == maxK)
            {
                curMax = right;
            }
            cnt += std::max(0, std::min(curMax, curMin) - left + 1); 
        }
        return cnt;
    }
```