# 132 Pattern

https://leetcode.com/problems/132-pattern

Given an array of n integers nums, a 132 pattern is a subsequence of three integers nums[i], nums[j] and nums[k] such that i < j < k and nums[i] < nums[k] < nums[j].

Return true if there is a 132 pattern in nums, otherwise, return false.

## Apporach 
``` C++
    bool find132pattern(vector<int>& nums) {
        if (nums.size() < 3)
        {
            return false;
        }
        
        std::stack<int> st;
        int k = INT_MIN;

        for (int i = nums.size() - 1; i >= 0; i--)
        {
            if (nums[i] < k)
            {   // Indicates we have one i, j, k which meet the requirement
                return true;
            }

            while (!st.empty() && nums[i] > st.top())
            {   // Make k large enough but still smaller than j, i.e: the nums[i]
                k = std::max(k, st.top());
                st.pop();
            }

            st.push(nums[i]);
        }
        return false;
    }
```