# Subarrays with K Different Integers

https://leetcode.com/problems/subarrays-with-k-different-integers/

Given an integer array nums and an integer k, return the number of good subarrays of nums.

A good array is an array where the number of different integers in that array is exactly k.

## Approach 

``` C++
    int atmost(std::vector<int>& nums, int k)
    {
        if (k == 0)
        {
            return 0;
        }
        int left = 0, right = 0;
        int cnt = 0;
        std::unordered_map<int, int> unique;
        while (right < nums.size())
        {
            unique[nums[right]]++;
            while (unique.size() > k)
            { // Current window has more than k unique integers, shrink the window
                unique[nums[left]]--;
                if (unique[nums[left]] == 0)
                {
                    unique.erase(nums[left]);
                }
                left++;
            }
            cnt += right - left + 1;
            right++;
        }
        return cnt;
    }

    int subarraysWithKDistinct(vector<int>& nums, int k) {
        return atmost(nums, k) - atmost(nums, k - 1);
    }
```