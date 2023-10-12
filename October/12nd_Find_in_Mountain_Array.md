# Find in Mountain Array

https://leetcode.com/problems/find-in-mountain-array

You may recall that an array arr is a mountain array if and only if:

arr.length >= 3
There exists some i with 0 < i < arr.length - 1 such that:
arr[0] < arr[1] < ... < arr[i - 1] < arr[i]
arr[i] > arr[i + 1] > ... > arr[arr.length - 1]
Given a mountain array mountainArr, return the minimum index such that mountainArr.get(index) == target. If such an index does not exist, return -1.

You cannot access the mountain array directly. You may only access the array using a MountainArray interface:

MountainArray.get(k) returns the element of the array at index k (0-indexed).
MountainArray.length() returns the length of the array.
Submissions making more than 100 calls to MountainArray.get will be judged Wrong Answer. Also, any solutions that attempt to circumvent the judge will result in disqualification.


## Approach 
``` C++
    int binarySearch(MountainArray& arr, int l, int r, int target, bool increase)
    {
        while (l <= r)
        {
            int mid = l + (r - l) / 2;
            if (increase)
            {
                if (arr.get(mid) < target)
                {
                    l = mid + 1;
                }
                else if (arr.get(mid) > target)
                {
                    r = mid - 1;
                }
                else
                {
                    return mid;
                }
            }
            else
            { // decreasing side
                if (arr.get(mid) > target)
                {
                    l = mid + 1;
                }
                else if (arr.get(mid) < target)
                {
                    r = mid - 1;
                }
                else
                {
                    return mid;
                }                
            }
        }
        return -1;
    }

    int findPeak(MountainArray& arr, int l, int r)
    {
        while (l < r)
        {
            int mid = l + (r - l) / 2;
            if (arr.get(mid) < arr.get(mid + 1))
            { // left side
                l = mid + 1;
            }
            else 
            { // right side
                r = mid;
            }
        }
        return l;
    }
    int findInMountainArray(int target, MountainArray &mountainArr) {
        int len = mountainArr.length();
        int l = 0;
        int r = len - 1;

        // Find the peak
        int peak = findPeak(mountainArr, l, r);

        if (target == mountainArr.get(peak))
        {
            return peak;
        }
        // Try left side first
        l = 0;
        r = peak;
        int ans = binarySearch(mountainArr, l, r, target, true);

        if (ans != -1)
        { // Found the target at left side
            return ans;
        }
        else
        { // Try right side
            l = peak;
            r = len - 1;
            ans = binarySearch(mountainArr, l, r, target, false);
            return ans;
        }     
    }
```