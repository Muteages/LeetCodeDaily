# Squares of a Sorted Array

Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.

## Approach 1

``` C++
    vector<int> sortedSquares(vector<int>& nums) {
        for (int& num : nums)
        {
            num *= num;
        }
        std::sort(nums.begin(), nums.end());
        return nums;
    }
```

## Approach 2

``` C++
    vector<int> sortedSquares(vector<int>& nums) {
        int n = nums.size();
        int l = 0, r = n - 1;
        std::vector<int> ans(n);
        for (int i = n - 1; i >= 0; i--)
        {
            if (std::abs(nums[r]) >= std::abs(nums[l]))
            {
                ans[i] = nums[r] * nums[r];
                r--;
            }
            else
            {
                ans[i] = nums[l] * nums[l];
                l++;
            }
        }
        return ans;
    }
```