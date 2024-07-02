# Intersection of Two Arrays

https://leetcode.com/problems/intersection-of-two-arrays-ii

Given two integer arrays nums1 and nums2, return an array of their intersection. Each element in the result must appear as many times as it shows in both arrays and you may return the result in any order.


## Approach 1

``` C++
    vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
        std::vector<int> freq(1001, 0);
        std::vector<int> ans;
        for (int num : nums1) 
        {
            freq[num]++;
        }
        for (int num : nums2) 
        {
            if (freq[num]-- > 0)
            {
                ans.emplace_back(num);
            }
        }
        return ans;
    }
```

``` JavaScript
var intersect = function(nums1, nums2) {
    const freq = {}, ans = [];
    nums1.forEach((num) => {
        freq[num] = (freq[num] || 0) + 1;
    });

    nums2.forEach((num) => {
        if (freq[num] && freq[num] > 0) {
            ans.push(num);
            freq[num]--;
        }
    })
    return ans;
};
```

## Approach 2

``` C++
    vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
        int n1 = nums1.size(), n2 = nums2.size();
        if (n1 < n2)
        {
            return intersect(nums2, nums1);
        }
        // Assume the arrays are sorted
        std::sort(nums1.begin(), nums1.end());
        std::sort(nums2.begin(), nums2.end());

        int i1 = 0, i2 = 0;
        std::vector<int> ans;
        while (i1 < n1 && i2 < n2)
        {
            if (nums1[i1] == nums2[i2])
            {
                ans.emplace_back(nums1[i1]);
                i1++;
                i2++;
            }
            else if (nums1[i1] < nums2[i2])
            {
                i1 = std::lower_bound(nums1.begin() + i1 + 1, nums1.end(), nums2[i2]) - nums1.begin();
            }
            else 
            {
                i2 = std::lower_bound(nums2.begin() + i2 + 1, nums2.end(), nums1[i1]) - nums2.begin();
            }
        }
        return ans;
    }
```


Implement binary search funciton
``` C++
    vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
        int n1 = nums1.size(), n2 = nums2.size();
        if (n1 < n2)
        {
            return intersect(nums2, nums1);
        }
        // Assume the arrays are sorted
        std::sort(nums1.begin(), nums1.end());
        std::sort(nums2.begin(), nums2.end());

        int i1 = 0, i2 = 0;
        std::vector<int> ans;
        while (i1 < n1 && i2 < n2)
        {
            if (nums1[i1] == nums2[i2])
            {
                ans.emplace_back(nums1[i1]);
                i1++;
                i2++;
            }
            else if (nums1[i1] < nums2[i2])
            {
                i1 = binarySearch(nums1, i1 + 1, n1, nums2[i2]);
            }
            else 
            {
                i2 = binarySearch(nums2, i2 + 1, n2, nums1[i1]);
            }
        }
        return ans;
    }

    int binarySearch(std::vector<int>& nums, int l, int r, int x)
    {
        while (l < r)
        {
            int m = l + (r - l) / 2;
            if (nums[m] < x)
            {
                l = m + 1;
            }
            else
            {
                break;
            }
        }
        return l;
    }
```
