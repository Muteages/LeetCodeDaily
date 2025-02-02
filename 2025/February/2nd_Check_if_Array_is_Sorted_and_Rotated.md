# Check if Array if Sorted and Rotated

https://leetcode.com/problems/check-if-array-is-sorted-and-rotated

Given an array nums, return true if the array was originally sorted in non-decreasing order, then rotated some number of positions (including zero). Otherwise, return false.

There may be duplicates in the original array.

Note: An array A rotated by x positions results in an array B of the same length such that A[i] == B[(i+x) % A.length], where % is the modulo operation.

## Approach 

``` C++
    bool check(vector<int>& nums) {
        int inversionCnt = 0; // Possible maximum inversion count is 1.
        int prev = nums.back();
        for (int num : nums)
        {
            if (num < prev)
            {
                inversionCnt++;
            }
            prev = num;
            if (inversionCnt > 1)
            {
                return false;
            }
        }
        return true;
    }
```

``` Python
    def check(self, nums: List[int]) -> bool:
        inversion_count = sum(x > y for (x, y) in pairwise(nums))
        inversion_count += nums[-1] > nums[0]
        return inversion_count <= 1
```

``` JavaScript
var check = function(nums) {
    let inversionCnt = 0;
    for (let i = 0; i < nums.length && inversionCnt <= 1; i++) {
        if (nums[i] > nums[(i + 1) % nums.length]) {
            inversionCnt++;
        }
    }
    return inversionCnt <= 1;
};
```