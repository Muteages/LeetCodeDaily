# Continuous Subarray Sum

https://leetcode.com/problems/continuous-subarray-sum

Given an integer array nums and an integer k, return true if nums has a good subarray or false otherwise.

A good subarray is a subarray where:

its length is at least two, and
the sum of the elements of the subarray is a multiple of k.
Note that:

A subarray is a contiguous part of the array.
An integer x is a multiple of k if there exists an integer n such that x = n * k. 0 is always a multiple of k.

## Approach 

Prefix
``` C++
    bool checkSubarraySum(vector<int>& nums, int k) {
        const int n = nums.size();
        if (n < 2)
        {
            return false;
        }
        int prefixSumMod = 0;
        std::unordered_map<int, int> ump; // prefixSumMod - idx
        ump[0] = -1;
        for (int i = 0; i < n; i++)
        {
            prefixSumMod = (prefixSumMod + nums[i]) % k;
            if (!ump.count(prefixSumMod)) 
            {
                ump[prefixSumMod] = i;
            }
            else if (i - ump[prefixSumMod] > 1)
            {
                return true;
            }
        }
        return false;
    }
```

``` JavaScript
var checkSubarraySum = function(nums, k) {
    const n = nums.length;
    let remList = new HashSet();
    let prefix = 0, prev = 0;
    for (let num of nums) {
        prefix = (prefix + num) % k;
        if (remList.has(prefix)) {
            return true;
        }
        remList.add(prev);
        prev = prefix;
    }
    return false;
};
```


## Approach 2

Using Unordered set instead. Maintain a extra variable prev to postphone insert mod by 1 step, avoid the effect caused by '0' element.

``` C++
    bool checkSubarraySum(vector<int>& nums, int k) {
        const int n = nums.size();
        if (n < 2)
        {
            return false;
        }
        int prefixSumMod = 0, prev = 0; // Maintain a prev variable to postphone insert mod by 1 step, avoid the effect caused by '0' element  
        std::unordered_set<int> us;
        for (int num : nums)
        {
            prefixSumMod = (prefixSumMod + num) % k;
            if (us.count(prefixSumMod))
            {
                return true;
            }
            us.emplace(prev);
            prev = prefixSumMod;
        }
        return false;
    }
```