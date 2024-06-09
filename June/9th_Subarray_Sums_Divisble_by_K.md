# Subarray Sums Divisible by K

https://leetcode.com/problems/subarray-sums-divisible-by-k

Given an integer array nums and an integer k, return the number of non-empty subarrays that have a sum divisible by k.

A subarray is a contiguous part of an array.

## Approach 

``` C++
    int subarraysDivByK(vector<int>& nums, int k) {
        const int n = nums.size();
        std::vector<int> freq(k, 0);
        freq[0] = 1; // Handle the edge case that starting from zero index
        int prefixSumMod = 0, ans = 0;
        for (int num : nums)
        {
            prefixSumMod = (prefixSumMod + num) % k; 
            prefixSumMod = prefixSumMod < 0 ? prefixSumMod + k : prefixSumMod; // Avoid the effect caused by negative numbers
            ans += freq[prefixSumMod];
            freq[prefixSumMod]++;
        }
        return ans;
    }
```

