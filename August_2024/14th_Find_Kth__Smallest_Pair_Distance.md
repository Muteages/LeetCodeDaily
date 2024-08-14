# Find Kth Smallest Pair Distance

https://leetcode.com/problems/find-k-th-smallest-pair-distance

The distance of a pair of integers a and b is defined as the absolute difference between a and b.

Given an integer array nums and an integer k, return the kth smallest distance among all the pairs nums[i] and nums[j] where 0 <= i < j < nums.length.

## Approach 1

``` C++
    int smallestDistancePair(vector<int>& nums, int k) {
        const int n = nums.size();
        std::vector<int> diff;
        diff.reserve(n * (n - 1) / 2);
        for (int i = 0; i < n; i++)
        {
            for (int j = i + 1; j < n; j++)
            {
                diff.emplace_back(std::abs(nums[i] - nums[j]));
            }
        }
        std::nth_element(diff.begin(), diff.begin() + k - 1, diff.end());
        return diff[k - 1];
    }
```
## Approach 2

``` C++
    // count the number of pairs with difference <= diff
    int cntDiffs(vector<int>& nums, int diff, int k)
    {
        int n = nums.size(), cnt = 0;
        for (int l = 0, r = 1; r < n; r++)
        {
            while (l < r && nums[r] - nums[l] > diff)
            {
                l++;
            }
            cnt += r - l;
            if (cnt >= k)
            {
                break;
            }
        }
        return cnt;
    }

    int smallestDistancePair(vector<int>& nums, int k) {
        std::sort(nums.begin(), nums.end());
        int left = 0, right = nums.back() - nums.front();
        while (left <= right)
        {
            int mid = left + (right - left) / 2;
            if (cntDiffs(nums, mid, k) < k)
            {
                left = mid + 1;
            }
            else
            {
                right = mid - 1;
            }
        }
        return left;
    }
```

