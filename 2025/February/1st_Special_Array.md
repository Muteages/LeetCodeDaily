# Special Array

https://leetcode.com/problems/special-array-i

An array is considered special if every pair of its adjacent elements contains two numbers with different parity.

You are given an array of integers nums. Return true if nums is a special array, otherwise, return false.

## Approach 

``` C++
    bool isArraySpecial(vector<int>& nums) {
        
        for (int i = 1; i < nums.size(); i++)
        {
            if (!(1 & (nums[i - 1] ^ nums[i]))) return false;
        }
        return true;
    }
```

``` Python
    def isArraySpecial(self, nums: List[int]) -> bool:
        return all(1 & (nums[i - 1]^ nums[i])  for i in range(1, len(nums)))
```

``` JavaScript
var isArraySpecial = function(nums) {
    return nums.every((num, i) => i === 0 || (nums[i - 1] ^ num) & 1);
};
```