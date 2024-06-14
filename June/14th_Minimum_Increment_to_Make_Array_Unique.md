# Minimum Increment to Make Array Unique

https://leetcode.com/problems/minimum-increment-to-make-array-unique/

You are given an integer array nums. In one move, you can pick an index i where 0 <= i < nums.length and increment nums[i] by 1.

Return the minimum number of moves to make every value in nums unique.

The test cases are generated so that the answer fits in a 32-bit integer.

## Approach 1

``` C++
    int minIncrementForUnique(vector<int>& nums) {
        std::vector<int> freq(1e5 + 1, 0);
        //int freq[100001] = {0};
        int maxNum = 0, minNum = 1e5 + 1, ans = 0;
        for (int num : nums)
        {
            freq[num]++;
            maxNum = std::max(maxNum, num);
            minNum = std::min(minNum, num);
        }
        for (int i = minNum; i < maxNum; ++i)
        {
            if (freq[i] <= 1)
            {
                continue;
            }
            int carry = freq[i] - 1; // Just keep one num and move others to next position
            ans += carry;
            freq[i + 1] += carry;
        }

        int rem = freq[maxNum] - 1;
        ans += rem * (rem + 1) / 2;
        return ans;
    }
```

## Approach 2

``` JavaScript
var minIncrementForUnique = function(nums) {
    nums.sort((a, b) => a - b);
    let possible = 0, ans = 0;
    for (let num of nums) {
        possible = Math.max(possible, num); // Find the maximum possible position to insert the current number
        ans += possible - num;              // Calculate the increment required to make the current number unique
        possible++;
    }
    return ans;
};
```