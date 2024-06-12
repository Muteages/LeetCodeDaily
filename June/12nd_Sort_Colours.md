# Sort Colours

https://leetcode.com/problems/sort-colors

Given an array nums with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers 0, 1, and 2 to represent the color red, white, and blue, respectively.

You must solve this problem without using the library's sort function.


## Approach 1

Counting Sort

``` C++
    void sortColors(vector<int>& nums) {
        std::vector<int> freq(3, 0);
        for (int num : nums)
        {
            freq[num]++;
        }

        int idx = 0;
        for (int i = 0; i < 3; ++i)
        {
            while (freq[i]--)
            {
                nums[idx++] = i;
            }
        }
    }
```

## Approach 2

Dutch Flag Algorithm

``` JavaScript
var sortColors = function(nums) {
    let l = 0, r = nums.length - 1, m = 0;
    while (m <= r) {
        if (nums[m] === 0) {
            [nums[l], nums[m]] = [nums[m], nums[l]];
            m++;
            l++;
        }
        else if (nums[m] === 1) {
            m++;
        }
        else {
            [nums[r], nums[m]] = [nums[m], nums[r]];
            r--;
        }
    }
};
```