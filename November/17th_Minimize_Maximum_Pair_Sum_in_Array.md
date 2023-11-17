# Minimize Maximum Pair Sum in Array

https://leetcode.com/problems/minimize-maximum-pair-sum-in-array

The pair sum of a pair (a,b) is equal to a + b. The maximum pair sum is the largest pair sum in a list of pairs.

## Approach 1

``` C++
    int minPairSum(vector<int>& nums) {
        std::sort(nums.begin(), nums.end());
        int i = 0, j = nums.size() - 1;
        int ans = INT_MIN;
        while (i < j)
        {
            ans = std::max(ans, nums[i++] + nums[j--]);
        }
        return ans;
    }
```

## Approach 2

``` C++
    int minPairSum(vector<int>& nums) {
        std::vector<int> freq(1e5 + 1, 0);
        int minNum = INT_MAX;
        int maxNum = INT_MIN;

        for (auto num : nums)
        {
            freq[num]++;
            minNum = std::min(minNum, num);
            maxNum = std::max(maxNum, num);
        }

        int ans = INT_MIN;
        while (minNum <= maxNum)
        {
            if (freq[minNum] == 0)
            {
                minNum++;
            }
            else if (freq[maxNum] == 0)
            {
                maxNum--;
            }
            else
            {
                ans = std::max(ans, minNum + maxNum);
                freq[minNum]--;
                freq[maxNum]--;
            }
        }
        return ans;
    }
```
