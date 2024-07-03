# Minimum Difference Between Largest and Smallest Value in Three Moves

https://leetcode.com/problems/minimum-difference-between-largest-and-smallest-value-in-three-moves

You are given an integer array nums.

In one move, you can choose one element of nums and change it to any value.

Return the minimum difference between the largest and smallest value of nums after performing at most three moves.

## Approach 1

``` C++
    int minDifference(vector<int>& nums) {
        const int n = nums.size();
        if (n <= 4)
        {
            return 0;
        }
        std::sort(nums.begin(), nums.end());
        int c1 = nums[n - 1] - nums[3],
            c2 = nums[n - 4] - nums[0],
            c3 = nums[n - 2] - nums[2],
            c4 = nums[n - 3] - nums[1];
        return std::min({c1, c2, c3, c4});
    }
```

## Approach 2

General solution for a variable number of moves.

``` C++
    int minDifference(vector<int>& nums, int k = 3) {
        const int n = nums.size();
        if (n <= k + 1)
        {
            return 0;
        }
        std::sort(nums.begin(), nums.end());
        int ans = INT_MAX, temp{};
        for (int i = 0; i <= k; i++)
        {
            temp = nums[n - 1 - i] - nums[k - i];
            ans = std::min(ans, temp);
        }
        return ans;
    }
```

## Approach 3

Avoid sorting the whole array

``` C++
    int minDifference(vector<int>& nums, int k = 3) {
        const int n = nums.size();
        if (n <= k + 1)
        {
            return 0;
        }

        std::nth_element(nums.begin(), nums.begin() + k , nums.end());
        std::sort(nums.begin(), nums.begin() + k);
        std::nth_element(nums.begin() + k + 1, nums.end() - 1 - k, nums.end());
        std::sort(nums.end() - k - 1, nums.end());
        int ans = INT_MAX;
        for (int i = 0; i <= k; i++)
        {
            ans = std::min(ans, nums[n - 1 - i] - nums[k - i]);
        }
        return ans;
    }
```
