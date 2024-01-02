# Convert an Array Into a 2D Array With Conditions

https://leetcode.com/problems/convert-an-array-into-a-2d-array-with-conditions

You are given an integer array nums. You need to create a 2D array from nums satisfying the following conditions:

The 2D array should contain only the elements of the array nums.
Each row in the 2D array contains distinct integers.
The number of rows in the 2D array should be minimal.
Return the resulting array. If there are multiple answers, return any of them.

Note that the 2D array can have a different number of elements on each row.

## Approach 1

``` C++
    vector<vector<int>> findMatrix(vector<int>& nums) {
        std::vector<std::vector<int>> ans;
        std::vector<int> freq(201);

        for (const int& num : nums)
        {
            if (freq[num] == ans.size())
            {
                ans.push_back({});
            }
            ans[freq[num]].emplace_back(num);
            freq[num]++;
        }
        return ans;
    }
```

## Approach 2

``` C++
   vector<vector<int>> findMatrix(vector<int>& nums) {
       std::unordered_map<int, int> freq;
       int m = 1;
       for (const int& num : nums)
       {
           freq[num]++;
           m = std::max(m, freq[num]);
       }
       std::vector<std::vector<int>> ans(m);
       for (const auto& [num, f] : freq)
       {
           for (int i = 0; i < f; i++)
           {
               ans[i].emplace_back(num);
           }
       }
       return ans;
    }
```