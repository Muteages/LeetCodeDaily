# Find Polygon With the Largest Perimeter

https://leetcode.com/problems/find-polygon-with-the-largest-perimeter

You are given an array of positive integers nums of length n.

A polygon is a closed plane figure that has at least 3 sides. The longest side of a polygon is smaller than the sum of its other sides.

The perimeter of a polygon is the sum of lengths of its sides.

Return the largest possible perimeter of a polygon whose sides can be formed from nums, or -1 if it is not possible to create a polygon.

## Approach 1

Forward iteration
``` C++
    long long largestPerimeter(vector<int>& nums) {
        std::sort(nums.begin(), nums.end());
        int n = nums.size();
        long long sum = nums[0];
        long long ans = -1;
        for (int i = 1; i < n; i++)
        {
            if (sum > nums[i])
            {
                ans = sum + nums[i];
            }
            sum += nums[i];
        }
        return ans;
    }
```

## Approach 2

Backward iteration

``` C++
    long long largestPerimeter(vector<int>& nums) {
        std::sort(nums.begin(), nums.end());
        long long sum = std::accumulate(nums.begin(), nums.end(), (long long)0);
        for (int i = nums.size() - 1; i > 1; i--)
        {
            sum -= nums[i];
            if (nums[i] < sum)
            {
                return sum + nums[i];
            }
        }
        return -1;
    }
```
