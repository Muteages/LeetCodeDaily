# Largest Positive Integer that Exists with Its Negative

https://leetcode.com/problems/largest-positive-integer-that-exists-with-its-negative

Given an integer array nums that does not contain any zeros, find the largest positive integer k such that -k also exists in the array.

Return the positive integer k. If there is no such integer, return -1.



## Approach 1

``` C++
    int findMaxK(vector<int>& nums) {
        std::sort(nums.begin(), nums.end());
        int left = 0, right = nums.size() - 1;
        while (left < right)
        {
            if (nums[left] > 0 || nums[right] < 0)
            { // Impossible to find the target
                break;
            }
            if (-nums[left] == nums[right])
            {
                return nums[right];
            }
            else if (-nums[left] < nums[right])
            {
                right--;
            }
            else
            {
                left++;
            }
        }
        return -1;
    }
```

## Approach 2

``` C++
    int findMaxK(vector<int>& nums) {
        std::vector<int8_t> visited(1001);
        int ans = -1;
        for (int num : nums)
        {
            if (num < 0)
            {
                num = -num;
                visited[num] |= 1; // Set 1 indicates we find negative number
            }
            else 
            {
                visited[num] |= 2; // Set 2 indicates we find positive number
            }
            if (visited[num] == 3 && num > ans)
            { // Set 3 indicates we have both negative and positive number for current element
                ans = num;
            }
        }
        return ans;
    }
```