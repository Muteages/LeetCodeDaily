# Longest Continuous Subarray with Absolute Diff Less than or Equal to Limit

https://leetcode.com/problems/longest-continuous-subarray-with-absolute-diff-less-than-or-equal-to-limit

Given an array of integers nums and an integer limit, return the size of the longest non-empty subarray such that the absolute difference between any two elements of this subarray is less than or equal to limit.

## Approach 1 

``` C++
    int longestSubarray(vector<int>& nums, int limit) {
        const int n = nums.size();
        int ans = 1, left = 0, right = 0;
        std::multiset<int> ms;
        for (int left = 0, right = 0; right < n; right++)
        {
            ms.insert(nums[right]);
            while (left <= right && (*ms.rbegin() - *ms.begin()) > limit)
            { // Out of boundary, move left pointer
                ms.erase(ms.find(nums[left++]));
            }
            ans = std::max(ans, right - left + 1);
        }
        return ans;
    }
```

## Approach 2

Maintain two heaps.

``` JavaScript
var longestSubarray = function(nums, limit) {
    let minHeap = [], maxHeap = [], ans = 1;
    const n = nums.length;
    for (let left = 0, right = 0; right < n; right++) {
        let num = nums[right];
        while (minHeap.length !== 0 && minHeap[minHeap.length - 1] > num) {
            minHeap.pop();
        }
        minHeap.push(num);

        while (maxHeap.length !== 0 && maxHeap[maxHeap.length - 1] < num) {
            maxHeap.pop();
        }
        maxHeap.push(num);

        while (maxHeap[0] - minHeap[0] > limit) {
            if (nums[left] === maxHeap[0]) {
                maxHeap.shift();
            }
            if (nums[left] === minHeap[0]) {
                minHeap.shift();
            }
            left++;
        }
        ans = Math.max(ans, right - left + 1);
    }
    return ans;
};
```