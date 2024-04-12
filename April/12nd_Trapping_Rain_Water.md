# Trapping Rain Water

https://leetcode.com/problems/trapping-rain-water

Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.

## Approach

``` C++
    int trap(vector<int>& height) {
        int n = height.size();
        std::vector<int> left(n, 0), right(n, 0);
        left[0] = height[0];
        right[n - 1] = height[n - 1];

        for (int i = 1; i < n; i++)
        {
            left[i] = std::max(left[i - 1], height[i]);
        }
        for (int i = n - 2; i >= 0; i--)
        {
            right[i] = std::max(right[i + 1], height[i]);
        }

        int ans = 0;
        for (int i = 0; i < n; i++)
        {
            ans += std::min(left[i], right[i]) - height[i];
        }
        return ans;
    }
```

## Approach 2

``` C++
    int trap(vector<int>& height) {
        int maxL = -1, maxR = -1;
        int l = 0, r = height.size() - 1;
        int ans = 0;
        while (l < r)
        {
            if (height[l] < height[r])
            {
                maxL = std::max(maxL, height[l]);
                ans += maxL - height[l++];
            }
            else
            {
                maxR = std::max(maxR, height[r]);
                ans += maxR - height[r--];
            }
        }
        return ans;
    }
```