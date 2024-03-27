Subarray Product Less Than K

https://leetcode.com/problems/subarray-product-less-than-k/


Given an array of integers nums and an integer k, return the number of contiguous subarrays where the product of all the elements in the subarray is strictly less than k.


## Approach 
``` C++
    int numSubarrayProductLessThanK(vector<int>& nums, int k) {
        if (k <= 1)
        {
            return 0;
        }
        int n = nums.size();
        int left = 0, right = 0;
        int product = 1;
        int cnt = 0;
        while (right < n)
        {
            product *= nums[right];
            while (product >= k)
            { // Move left boundary
                product /= nums[left];
                left++;
            }
            cnt += right - left + 1;
            right++;
        }
        return cnt;
    }
```