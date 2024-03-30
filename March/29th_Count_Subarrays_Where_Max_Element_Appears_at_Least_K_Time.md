# Count Subarrays Where Max Element Appears at Least K Times

https://leetcode.com/problems/count-subarrays-where-max-element-appears-at-least-k-times

You are given an integer array nums and a positive integer k.

Return the number of subarrays where the maximum element of nums appears at least k times in that subarray.

## Approach 1

Math
``` C++
    long long countSubarrays(vector<int>& nums, int k) {
        const int maxNum = *max_element(nums.begin(), nums.end());
        int n = nums.size();
        std::vector<int> idx; // Store indices of maxNum in array
        idx.emplace_back(-1);
        for (int i = 0; i < n; ++i)
        {
            if (maxNum == nums[i])
            {
                idx.emplace_back(i);
            }
        }
        if (idx.size() < k)
        { // Can't build the target subarray
            return 0;
        }
        long long count = 0;
        for (int i = 1; i <= idx.size() - k; i++)
        {
            count += static_cast<long long>(idx[i] - idx[i - 1]) * (n - idx[i + k - 1]); // prefix * suffix
        }
        return count;
    }
```

## Approach 2

Sliding Window

``` C++
    long long countSubarrays(vector<int>& nums, int k) {
        const int maxNum = *max_element(nums.begin(), nums.end());
        int n = nums.size();
        int left = 0, right = 0, cnt = 0;
        long long ans = 0;
        while (right < n)
        {
            cnt += (nums[right] == maxNum);
            while (cnt == k)
            {
                cnt -= (nums[left] == maxNum);
                left++;
                ans += n - right;
            }
            right++;
        }
        return ans;
    }
```

## Approach 3

Total Subarrays count substract atmost k-1 subarrays with max element

``` C++
    long long atmost(vector<int>& nums, int k, int MAX)
    {
        long long cnt = 0;
        int left = 0, right = 0;
        int maxNum = 0;
        while (right < nums.size())
        {
            maxNum += nums[right] == MAX;
            while (left <= right && maxNum > k)
            {
                maxNum -= nums[left] == MAX;
                left++;
            }
            cnt += (long long)right - left + 1;
            right++;
        }
        return cnt;
    }
    long long countSubarrays(vector<int>& nums, int k) {
        const int MAX = *max_element(nums.begin(), nums.end());
        int n = nums.size();
        long long total = (long long)n * (n + 1) / 2;
        return total - atmost(nums, k - 1, MAX);
    }
```
