# Minimum Swaps to Group All 1's Together II

https://leetcode.com/problems/minimum-swaps-to-group-all-1s-together-ii

A swap is defined as taking two distinct positions in an array and swapping the values in them.

A circular array is defined as an array where we consider the first element and the last element to be adjacent.

Given a binary circular array nums, return the minimum number of swaps required to group all 1's present in the array together at any location.

## Approach 

``` C++
    int minSwaps(vector<int>& nums) {
        const int total = std::count(nums.begin(), nums.end(), 1), n = nums.size();
        if (total == 0 || total == n) return 0;
        int cur1s = 0, ans = n;
        for (int left = 0, right = 0; right < n + total; right++)
        {
            cur1s += nums[right % n];
            if (right - left + 1 > total)
            {
                cur1s -= nums[left % n];
                left++;
            }
            if (right - left + 1 == total)
            {
                ans = std::min(ans, total - cur1s);
            }
        }
        return ans;
    }
```