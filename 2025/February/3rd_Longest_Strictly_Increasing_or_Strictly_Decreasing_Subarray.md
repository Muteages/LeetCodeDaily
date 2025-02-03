# Longest Strictly Increasing or Strictly Decreasing Subarray

https://leetcode.com/problems/longest-strictly-increasing-or-strictly-decreasing-subarray


## Approach 

``` C++
    int longestMonotonicSubarray(vector<int>& nums) {
        const int n = nums.size();
        if (n == 1) return 1;
        int incLen = 1, decLen = 1, ans = 1;
        for (int i = 1; i < n; i++)
        {
            if (nums[i] > nums[i - 1])
            {
                incLen++;
                decLen = 1;
            }
            else if (nums[i] < nums[i - 1])
            {
                decLen++;
                incLen = 1;
            }
            else
            { // nums[i] == nums[i - 1]
                incLen = 1;
                decLen = 1;
            }
            ans = std::max({incLen, decLen, ans});
        }
        return ans;
    }
```


``` Python
    def longestMonotonicSubarray(self, nums: List[int]) -> int:
        inc, dec, ans = 1, 1, 1
        for x, y in pairwise(nums):
            if x < y:
                inc += 1
                dec = 1
            elif x > y:
                inc = 1
                dec += 1
            else:
                inc = dec = 1

            ans = max(ans, inc, dec)
        return ans
```

``` JavaScript

```