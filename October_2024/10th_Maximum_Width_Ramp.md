# Maximum Width Ramp

https://leetcode.com/problems/maximum-width-ramp

A ramp in an integer array nums is a pair (i, j) for which i < j and nums[i] <= nums[j]. The width of such a ramp is j - i.

Given an integer array nums, return the maximum width of a ramp in nums. If there is no ramp in nums, return 0.

## Approach 1

Optimised brute force. Got TLE for large cases.

``` C++
    int maxWidthRamp(vector<int>& nums) {
        int n = nums.size() - 1;
        int ans = 0;
        int tempMax = -1;
        for (int j = n; j >= 0; j--)
        {
            if (j < ans) break; // Early exit
            if (nums[j] < tempMax) continue;
            for (int i = 0; i < j; i++)
            {
                if (j - i < ans) break;

                if (nums[j] >= nums[i])
                { // Find the ramp
                    ans = std::max(ans, j - i);
                    tempMax = std::max(tempMax, nums[j]);
                    break;
                }
            }
        }
        return ans;
    }
```

## Approach 2

``` C++
    int maxWidthRamp(vector<int>& nums) {
        const int n = nums.size();
        std::vector<std::pair<int, int>> v2i(n); // value - index
        for (int i = 0; i < n; i++)
        {
            v2i[i] = {nums[i], i};
        }
        std::sort(v2i.begin(), v2i.end());

        int minIndex = n, maxWidth = 0;
        for (int i = 0; i < n; i++)
        {
            maxWidth = std::max(maxWidth, v2i[i].second - minIndex);
            minIndex = std::min(minIndex, v2i[i].second);
        }
        return maxWidth;
    }
```

