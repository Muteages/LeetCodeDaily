# Maximum Score of a Good Subarray

https://leetcode.com/problems/maximum-score-of-a-good-subarray

You are given an array of integers nums (0-indexed) and an integer k.

The score of a subarray (i, j) is defined as min(nums[i], nums[i+1], ..., nums[j]) * (j - i + 1). A good subarray is a subarray where i <= k <= j.

Return the maximum possible score of a good subarray.

## Approach 

``` C++
    int maximumScore(vector<int>& nums, int k) {
        int i = k, j = k;
        int minNum = nums[k];
        int maxScore = minNum; // minNum * (j - i + 1)

        while (i > 0 || j < nums.size() - 1)
        {
            if (i == 0 || (j < nums.size() - 1 && nums[j + 1] > nums[i - 1]))
            {
                j++;
            }
            else
            {
                i--;
            }

            minNum = std::min({minNum, nums[i], nums[j]});
            int curScore = minNum * (j - i + 1);
            maxScore = std::max(maxScore, curScore);
        }
        return maxScore;
    }
```