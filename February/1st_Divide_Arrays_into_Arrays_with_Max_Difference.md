# Divide Array Into Arrays With Max Difference

https://leetcode.com/problems/divide-array-into-arrays-with-max-difference

You are given an integer array nums of size n and a positive integer k.

Divide the array into one or more arrays of size 3 satisfying the following conditions:

Each element of nums should be in exactly one array.
The difference between any two elements in one array is less than or equal to k.
Return a 2D array containing all the arrays. If it is impossible to satisfy the conditions, return an empty array. And if there are multiple answers, return any of them.

## Approach

``` C++
    vector<vector<int>> divideArray(vector<int>& nums, int k) {
        std::sort(nums.begin(), nums.end());
        int n = nums.size();
        std::vector<std::vector<int>> ans(n / 3);
        int curr = 0;
        while (curr < n)
        {
            std::vector<int> temp(3);
            for (int i = 0; i < 3; i++)
            { // Build the current array
                temp[i] = nums[curr++];
            }
            if (temp[2] - temp[0] > k)
            { // The difference greater than k, i.e. fail to build the array
                return {};
            }
            ans[curr / 3 - 1] = temp;
        }
        return ans;
    }
```