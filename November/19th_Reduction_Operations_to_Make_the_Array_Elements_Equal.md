# Reduction Operations to Make the Array Elements Equal

https://leetcode.com/problems/reduction-operations-to-make-the-array-elements-equal

Given an integer array nums, your goal is to make all elements in nums equal. To complete one operation, follow these steps:

Find the largest value in nums. Let its index be i (0-indexed) and its value be largest. If there are multiple elements with the largest value, pick the smallest i.
Find the next largest value in nums strictly smaller than largest. Let its value be nextLargest.
Reduce nums[i] to nextLargest.
Return the number of operations to make all elements in nums equal.

## Approach 1

Count the frequency
``` C++
    int reductionOperations(vector<int>& nums) {
        std::map<int, int, std::greater<int>> frequency;
        for (auto num : nums)
        {
            frequency[num]++;
        }

        frequency.erase(std::prev(frequency.end())); // We don't need to count the last element since they are the smallest already.
        int ans = 0;
        int totalCnt = 0; // Store count of the current element
        for (auto [num, cnt] : frequency)
        {
            totalCnt += cnt; // previous + current 
            ans += totalCnt;
        }
        return ans;
    }
```

## Approach 2
``` C++
    int reductionOperations(vector<int>& nums) {
        std::sort(nums.begin(), nums.end(), std::greater<int>());
        int ans = 0;
        for (int i = 1; i < nums.size(); i++)
        {
            if (nums[i] != nums[i - 1])
            {
                ans += i;
            }
        }
        return ans;
    }
```