# Number of Good Pairs

https://leetcode.com/problems/number-of-good-pairs

Given an array of integers nums, return the number of good pairs.

A pair (i, j) is called good if nums[i] == nums[j] and i < j.

## Approach 1
Brute Force

``` C++
    int numIdenticalPairs(vector<int>& nums) {
        int cnt = 0;
        for (int i = 0; i < nums.size() - 1; i++)
        {
            for (int j = i + 1; j < nums.size(); j++)
            {
                if (nums[i] == nums[j])
                {
                    cnt++;
                }
            }
        }
        return cnt;
    }
```

## Approach 2
Frequencies

``` C++
    int numIdenticalPairs(vector<int>& nums) {
        std::unordered_map<int, int> freq;

        for (int& num : nums)
        {
            freq[num]++;
        }
        int cnt = 0;
        for (auto [num, f] : freq)
        {
            cnt += f * (f - 1) / 2;
        }
        return cnt;
    }
```