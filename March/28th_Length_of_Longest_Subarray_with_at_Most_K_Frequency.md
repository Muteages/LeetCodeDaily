# Length of Longest Subarray with at Most K Frequency

https://leetcode.com/problems/length-of-longest-subarray-with-at-most-k-frequency/


You are given an integer array nums and an integer k.

The frequency of an element x is the number of times it occurs in an array.

An array is called good if the frequency of each element in this array is less than or equal to k.

Return the length of the longest good subarray of nums.

## Approach 
``` C++
    int maxSubarrayLength(vector<int>& nums, int k) {
        std::unordered_map<int, int>freq;
        int maxSubarray = 0;
        int left = 0, right = 0;
        while (right < nums.size())
        {
            freq[nums[right]]++;
            while (freq[nums[right]] > k)
            {
                freq[nums[left]]--;
                left++;
            }
            maxSubarray = std::max(maxSubarray, right - left + 1);
            right++;
        }
        return maxSubarray;
    }
```