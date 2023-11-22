# Diagonal Traverse

https://leetcode.com/problems/diagonal-traverse-ii

Given a 2D integer array nums, return all elements of nums in diagonal order as shown in the below images.

## Approach 

``` C++
    vector<int> findDiagonalOrder(vector<vector<int>>& nums) {
        std::map<int, std::vector<std::tuple<int, int, int>>> diag;  //  tuple : col - row - val

        for (int row = 0; row < nums.size(); row++)
        {
            for (int col = 0; col < nums[row].size(); col++)
            {
                diag[row + col].emplace_back(col, row, nums[row][col]);
            }
        }

        std::vector<int> ans;
        for (auto& [sum, list] : diag)
        {
            std::sort(list.begin(), list.end()); // Make the list follow the order from left bottom to right top
            for (auto& [col, row, val] : list)
            {
                ans.emplace_back(val);
            }
        }
        return ans;
    }
```

Improve : avoid the tuple structure: store the elements from bottom to left. 
``` C++
       std::map<int, std::vector<int>> diag;

        for (int row = nums.size() - 1; row >= 0; row--)
        {
            for (int col = 0; col < nums[row].size(); col++)
            {
                diag[row + col].emplace_back(nums[row][col]);
            }
        }

        std::vector<int> ans;
        for (auto& [sum, list] : diag)
        {
            for (auto& val : list)
            {
                ans.emplace_back(val);
            }
        }
```