# Maximum Ascending Subarray Sum

https://leetcode.com/problems/maximum-ascending-subarray-sum

Given an array of positive integers nums, return the maximum possible sum of an ascending subarray in nums.

A subarray is defined as a contiguous sequence of numbers in an array.

## Approach 

``` Python
    def maxAscendingSum(self, nums: List[int]) -> int:
        ans = cur_sum = nums[0]
        for x, y in pairwise(nums):
            cur_sum = cur_sum + y if x < y else y
            ans = max(ans, cur_sum)
        return ans
```

``` C++
    int maxAscendingSum(vector<int>& nums) {
        int ans = nums[0], curSum = nums[0];
        for (int i = 1; i < nums.size(); i++)
        {
            curSum = (nums[i] > nums[i - 1]) ? curSum + nums[i] : nums[i];
            ans = std::max(ans, curSum);
        }
        return ans;
    }
```