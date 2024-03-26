# First Missing Positive

https://leetcode.com/problems/first-missing-positive/description/

Given an unsorted integer array nums. Return the smallest positive integer that is not present in nums.

You must implement an algorithm that runs in O(n) time and uses O(1) auxiliary space.

## Approach 1

``` C++
    int firstMissingPositive(vector<int>& nums) {
        int n = nums.size();
        nums.emplace_back(-1);
        for (int i = 0; i <= n; i++)
        {
            int& num = nums[i];
            while (num > 0 && num <= n && num != nums[num])
            {
                std::swap(num, nums[num]);
            }
        }

        for (int i = 1; i <= n; i++)
        {
            if (nums[i] != i)
            {
                return i;
            }
        }
        return n + 1;
    }
```


