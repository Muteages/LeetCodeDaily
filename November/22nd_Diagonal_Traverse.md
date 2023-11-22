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

## Approach 2

``` C++
    vector<int> findDiagonalOrder(vector<vector<int>>& nums) {
        std::vector<int> ans;
        int n = nums.size();
        std::queue<std::pair<int, int>> q;
        q.emplace(0, 0);

        while (!q.empty())
        {
            auto [row, col] = q.front();
            q.pop();
            ans.emplace_back(nums[row][col]);

            // Update node
            if (col == 0 && row + 1 < n)
            {   // Add the element below
                q.emplace(row + 1, 0);
            }
            if (col + 1 < nums[row].size())
            {   // Add the element on the right
                q.emplace(row, col + 1);
            }
        }
        return ans;
    }
```