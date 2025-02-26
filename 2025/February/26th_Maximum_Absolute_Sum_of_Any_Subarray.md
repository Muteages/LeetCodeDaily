# Maximum Absolute Sum of Any Subarray

You are given an integer array nums. The absolute sum of a subarray [numsl, numsl+1, ..., numsr-1, numsr] is abs(numsl + numsl+1 + ... + numsr-1 + numsr).

Return the maximum absolute sum of any (possibly empty) subarray of nums.

## Approach 1 

Kadane's algorithm

``` C++
    int maxAbsoluteSum(vector<int>& nums) {
        int maxSum = 0, minSum = 0, ans = 0;
        for (int num : nums)
        {
            maxSum = std::max(maxSum + num, num);
            minSum = std::min(minSum + num, num);
            ans = std::max({ans, std::abs(maxSum), std::abs(minSum)});
        }
        return ans;
    }
```

``` Python
    def maxAbsoluteSum(self, nums: List[int]) -> int:
        max_sum = 0
        min_sum = 0
        curr_max_sum = 0
        curr_min_sum = 0
        for i in range(len(nums)):
            curr_max_sum = max(curr_max_sum + nums[i], nums[i])
            max_sum = max(max_sum, curr_max_sum)

            curr_min_sum = min(curr_min_sum + nums[i], nums[i])
            min_sum = min(min_sum, curr_min_sum)
        
        return max(abs(max_sum), abs(min_sum))
```

## Approach 2

Use prefix to find max sum and min sum.  maxSum - minSum = target

``` C++
    int maxAbsoluteSum(vector<int>& nums) {
        int maxSum = 0, minSum = 0;
        int curSum = 0;
        for (int num : nums)
        {
            curSum += num;
            maxSum = std::max(maxSum, curSum);
            minSum = std::min(minSum, curSum);
        }
        return maxSum - minSum;
    }
```

``` Python
    def maxAbsoluteSum(self, nums: List[int]) -> int:
        prefix = list(accumulate(nums, initial = 0))
        return max(prefix) - min(prefix)   
```

``` JavaScript
var maxAbsoluteSum = function(nums) {
    let prefix = 0;
    nums = nums.map((ele) => prefix = prefix + ele);
    return Math.max(...nums, 0) - Math.min(...nums, 0);
};
```