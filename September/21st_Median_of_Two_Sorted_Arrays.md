# Median of Two Sorted Arrays

https://leetcode.com/problems/median-of-two-sorted-arrays/description

Given two sorted arrays nums1 and nums2 of size m and n respectively, return the median of the two sorted arrays.


## Approach 1

With sort function

``` C++
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        nums1.insert(nums1.end(), nums2.begin(), nums2.end());
        int n = nums1.size();
        std::sort(nums1.begin(), nums1.end());
        if (n % 2 == 0)
        {
            return (double)(nums1[n / 2 - 1] + nums1[n / 2]) * (double)0.5;
        }
        else
        {
            return (double)(nums1[n / 2]);
        }
    }
```

## Approach 2 

Without sort function

``` C++
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        std::vector<int> merged(nums1.size() + nums2.size());
        int idx1 = 0, idx2 = 0;
        int n = merged.size();

        for (int i = 0; i < n; i++)
        {
            if (idx1 < nums1.size() && (idx2 == nums2.size() || nums1[idx1] < nums2[idx2]))
            {
                merged[i] = nums1[idx1];
                idx1++;
            }
            else
            {
                merged[i] = nums2[idx2];
                idx2++;
            }
        }

        if (n % 2 == 0)
        {
            return (double)(merged[n / 2 - 1] + merged[n / 2]) * 0.5;
        }
        else
        {
            return (double)(merged[n / 2]);
        }
    }
```