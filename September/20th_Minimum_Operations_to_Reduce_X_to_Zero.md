# Minimum Operations to Reduce X to Zero

https://leetcode.com/problems/minimum-operations-to-reduce-x-to-zero

You are given an integer array nums and an integer x. In one operation, you can either remove the leftmost or the rightmost element from the array nums and subtract its value from x. Note that this modifies the array for future operations.

Return the minimum number of operations to reduce x to exactly 0 if it is possible, otherwise, return -1.

## Approach 

``` C++
    int minOperations(vector<int>& nums, int x) {
        if (nums.front() > x && nums.back() > x)
        {
            return -1;
        }
        int n = nums.size();
        int target = std::accumulate(nums.begin(), nums.end(), 0) - x;
        if (target == 0)
        { // Indicates all elements need to be removed 
            return n;
        }
        else if (target < 0)
        { // Failed to make x to zero
            return -1;
        }

        int curSum = 0;
        int left = 0, right = 0;
        int len = 0;
        while (right < n)
        { // Sliding window
            curSum += nums[right];

            while (curSum > target)
            {
                curSum -= nums[left];
                left++;
            }

            if (curSum == target)
            { // Max subarry 
                len = std::max(len, right - left + 1);
            }
            right++;
        }

        return len ? n - len : -1;
    }
```