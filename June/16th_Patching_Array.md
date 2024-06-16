# Patching Array

https://leetcode.com/problems/patching-array/

Given a sorted integer array nums and an integer n, add/patch elements to the array such that any number in the range [1, n] inclusive can be formed by the sum of some elements in the array.

Return the minimum number of patches required.


## Approach

``` C++
    int minPatches(vector<int>& nums, int n) {
        const int sz = nums.size();
        int i = 0, cnt = 0;
        long long sum = 0;
        while (sum < n)
        {
            if (i < sz && nums[i] <= sum + 1)
            { // Indicates that [1, nums[i]] elements can be formed
                sum += nums[i];
                i++;
            }
            else
            {
                sum += sum + 1; // Need to add a new element which equals to "sum + 1" to fill the gap, otherwise we can't form the number "sum + 1"
                cnt++;
            }
        }
        return cnt;
    }
```

``` JavaScript
var minPatches = function(nums, n) {
    let ans = 0, sum = 0, i = 0;
    const sz = nums.length;
    while (sum < n) {
        if (i < sz && nums[i] <= sum + 1) {
            sum += nums[i++];
        } else {
            ans++;
            sum += sum + 1;
        }
    }
    return ans;
};
```
