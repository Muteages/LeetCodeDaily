# Maximum Product Difference Between Two Pairs

https://leetcode.com/problems/maximum-product-difference-between-two-pairs

The product difference between two pairs (a, b) and (c, d) is defined as (a * b) - (c * d).

Return the maximum such product difference.

## Approach 1

Sort
``` C++
    int maxProductDifference(vector<int>& nums) {
        std::sort(nums.begin(), nums.end());
        int n = nums.size();
        int w = nums[n - 1];
        int x = nums[n - 2];
        int y = nums[0];
        int z = nums[1];
        int ans = w * x - y * z;
        return ans;
    }
```

## Approach 2

Traverse the vector and track four elements
``` C++
   int maxProductDifference(vector<int>& nums) {
        int w{0}, x{0}, y{10001}, z{10001};
        for (int num : nums)
        {
            if (num > w)
            { // The biggest number
                x = w;
                w = num;
            }
            else if (num > x)
            {
                x = num;
            }
            if (num < z)
            { // The smallest number
                y = z;
                z = num;
            }
            else if (num < y)
            {
                y = num;
            }
        }
        int ans = w * x - y * z;
        return ans;
    }
```
