# Binary Subarrays with Sum

https://leetcode.com/problems/binary-subarrays-with-sum

Given a binary array nums and an integer goal, return the number of non-empty subarrays with a sum goal.

A subarray is a contiguous part of the array.

## Approach 1

Brute force, get TLE for large cases

``` C++
    int numSubarraysWithSum(vector<int>& nums, int goal) {
        int ans{};
        for (int i = 0; i < nums.size(); i++)
        {
            int sum = 0;
            for (int j = i; j < nums.size(); j++)
            {
                sum += nums[j];
                if (sum == goal)
                {
                    ans++;
                }
                else if (sum > goal)
                {
                    break;
                }
            }
        }
        return ans;
    }
```

## Approach 2

Sliding window
``` C++
    int atmostSum(vector<int>& nums, int goal) {
        int cnt = 0;
        int sum = 0;
        int left = 0, right = 0;
        while (right < nums.size())
        {
            sum += nums[right];
            while (sum > goal && left <= right)
            {
                sum -= nums[left];
                left++;
            }
            cnt += right - left + 1;
            right++;
        }
        return cnt;
    }
    int numSubarraysWithSum(vector<int>& nums, int goal) {
        return goal > 0 ? atmostSum(nums, goal) - atmostSum(nums, goal - 1) : atmostSum(nums, goal);
    }
```