# The Number of Beautiful Subsets

https://leetcode.com/problems/the-number-of-beautiful-subsets

You are given an array nums of positive integers and a positive integer k.

A subset of nums is beautiful if it does not contain two integers with an absolute difference equal to k.

Return the number of non-empty beautiful subsets of the array nums.

A subset of nums is an array that can be obtained by deleting some (possibly none) elements from nums. Two subsets are different if and only if the chosen indices to delete are different.

## Approach 

``` C++
    int ans, n;
    std::vector<int> freq;
    int beautifulSubsets(vector<int>& nums, int k) {
        ans = 0;
        n = nums.size();
        freq.resize(1001, 0);
        backtrack(nums, k, 0);
        return ans - 1; // remove the empty subset
    }

    void backtrack(std::vector<int>& nums, int k, int idx)
    {
        if (idx == n)
        {
            ans++;
            return;
        }

        backtrack(nums, k, idx + 1); // Skip current element
        int curr = nums[idx];
        if ((curr - k < 0 || freq[curr - k] == 0) && (curr + k > 1000 || freq[curr + k] == 0))
        { // Include current element
            freq[curr]++;
            backtrack(nums, k, idx + 1);
            freq[curr]--;
        }
    }
```