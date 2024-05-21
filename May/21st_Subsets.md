# Subsets

https://leetcode.com/problems/subsets

Given an integer array nums of unique elements, return all possible subsets (the power set).


## Approach 1

Backtracking
``` C++
    std::vector<std::vector<int>> ans;

    void getSubset(std::vector<int>& nums, std::vector<int>& curr, int idx)
    {
        ans.emplace_back(curr);
        for (int i = idx; i < nums.size(); i++)
        {
            curr.emplace_back(nums[i]);
            getSubset(nums, curr, i + 1);
            curr.pop_back();
        }
    }
    vector<vector<int>> subsets(vector<int>& nums) {
        ans.reserve(1 << nums.size()); 
        std::vector<int> curr{};
        getSubset(nums, curr, 0);
        return ans;
    }
```

## Approach 2

Bit manipulation

``` C++
    vector<vector<int>> subsets(vector<int>& nums) {
        int sz = 1 << nums.size(); // 2^n subsets
        std::vector<std::vector<int>> ans(sz);
        for (int i = 0; i < sz; i++)
        {
            ans[i].reserve(__builtin_popcount(i));
            for (int j = 0; j < nums.size(); j++)
            {
                if (i & 1 << j)
                { // Check if jth bit is set in i
                    ans[i].emplace_back(nums[j]);
                }
            }
        }
        return ans;
    }
```

## Approach 3

``` C++
    vector<vector<int>> subsets(vector<int>& nums) {
        std::vector<std::vector<int>> ans;
        int n = nums.size();
        ans.reserve(1 << n);
        ans.emplace_back();
        for (int num : nums)
        {
            int sz = ans.size();
            for (int i = 0; i < sz; i++)
            {
                auto curr = ans[i];
                curr.emplace_back(num);
                ans.emplace_back(std::move(curr));
            }
        }
        return ans;
    }
```