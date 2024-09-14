# Longest Subarray with Maximum Bitwise AND



## Approach 1

2 passes approach
``` C++
    int longestSubarray(vector<int>& nums) {
        int maxi = *std::max_element(nums.begin(), nums.end());
        int n = nums.size();
        int ans = 1;
        for (int i = 0; i < n; i++)
        {
            int len = 0;
            while (i < n && nums[i] == maxi)
            {
                len++;
                i++;
            }
            ans = std::max(ans, len);
        }
        return ans;
    }
```

## Approach 2

1 pass approach

``` JavaScript
var longestSubarray = function(nums) {
    let maxLen = 0, len = 0, maxNum = 0;
    for (let num of nums) {
        if (num > maxNum) {
            maxNum = num;
            len = 1;
            maxLen = 1;
        }
        else if (num === maxNum) {
            len++;
        }
        else {
            maxLen = Math.max(len, maxLen);
            len = 0;
        }
    }
    return Math.max(maxLen, len);
};
```

``` JavaScript
var longestSubarray = function(nums) {
    let max = 0, ans = 1, n = nums.length;
    for (let i = 0; i < n;) {

        // Step 1: find the current biggest number
        while (i < n && nums[i] < max) {
            i++;
        }
        if (i === n) break;
        if (nums[i] > max) {
            max = nums[i];
            ans = 1;
        }
        let len = 0;
        // Step 2: find the current longest subarray
        while (i < n && nums[i] === max) {
            len++;
            i++;
        }
        ans = Math.max(ans, len);
    }
    return ans;
};
```

