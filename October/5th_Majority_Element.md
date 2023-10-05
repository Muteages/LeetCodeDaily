# Majority Element

https://leetcode.com/problems/majority-element-ii

Given an integer array of size n, find all elements that appear more than ⌊ n/3 ⌋ times.

## Approach 1
``` C++
    vector<int> majorityElement(vector<int>& nums) {
        int t = std::floor( nums.size() / 3);
        std::unordered_map<int, int> freq;
        for (int num& : nums)
        {
            freq[num]++;
        }

        std::vector<int> ans;
        for (auto& [num, f] : freq)
        {
            if (f > t)
            {
                ans.push_back(num);
            }
        }
        return ans;
    }
```

## Approach 2

``` C++
    vector<int> majorityElement(vector<int>& nums) {
        std::sort(nums.begin(), nums.end());
        int t = std::floor(nums.size() / 3);
        int freq = 1;
        std::vector<int> ans;
        for (int i = 1; i < nums.size(); i++)
        {
            if (nums[i] == nums[i - 1])
            { // Record current number frequency
                freq++;
            }
            else
            {
                if (freq > t)
                {
                    ans.push_back(nums[i - 1]);
                }
                freq = 1;
            }
        }

        if (freq > t)
        { // Edge case: the last number's occurrences is greater than t 
            ans.push_back(nums.back());
        }

        return ans;
    }
```

## Approach 3

Boyer-Moore Majority Voting Alogrithm

``` C++
    vector<int> majorityElement(vector<int>& nums) {
        int candidate1 = INT_MIN, candidate2 = INT_MIN;
        int cnt1 = 0, cnt2 = 0;
        for (int& num : nums)
        {
            if (num == candidate1)
            {
                cnt1++;
            }
            else if (num == candidate2)
            {
                cnt2++;
            }
            else if (cnt1 == 0)
            {
                candidate1 = num;
                cnt1 = 1;
            }
            else if (cnt2 == 0)
            {
                candidate2 = num;
                cnt2 = 1;
            }
            else
            { // If the current number is different from two candidates, decrease counts
                cnt1--;
                cnt2--;
            }
        }

        std::vector<int> ans;
        cnt1 = 0;
        cnt2 = 0;
        for (int& num : nums)
        {
            if (num == candidate1)
            {
                cnt1++;
            }
            else if (num == candidate2)
            {
                cnt2++;
            }
        }
        int t = nums.size() / 3;
        if (cnt1 > t)
        {
            ans.push_back(candidate1);
        }
        if (cnt2 > t)
        {
            ans.push_back(candidate2);
        }
        return ans;
    }
```
