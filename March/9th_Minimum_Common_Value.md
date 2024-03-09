# Minimum Common Value

Given two integer arrays nums1 and nums2, sorted in non-decreasing order, return the minimum integer common to both arrays. If there is no common integer amongst nums1 and nums2, return -1.

Note that an integer is said to be common to nums1 and nums2 if both arrays have at least one occurrence of that integer.

## Approach

``` C++
    int getCommon(vector<int>& nums1, vector<int>& nums2) {
        int idx1 = 0, idx2 = 0;
        while (idx1 < nums1.size() && idx2 < nums2.size())
        {
            if (nums1[idx1] == nums2[idx2])
            {
                return nums1[idx1];
            }
            if (nums1[idx1] < nums2[idx2])
            {
                idx1++;
            }
            else
            {
                idx2++;
            }
        }
        return -1;
    }
```