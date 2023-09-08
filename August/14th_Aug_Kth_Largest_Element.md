# 215. Kth Largest Element in an Array

https://leetcode.com/problems/kth-largest-element-in-an-array/description/

Given an integer array nums and an integer k, return the kth largest element in the array.

Note that it is the kth largest element in the sorted order, not the kth distinct element.


## Approach 1
Using map to record the frequencies of numbers and find the kth number.

``` C++
    int findKthLargest(vector<int>& nums, int k) {
        std::map<int, int, std::greater<int>> frequency; // number - frequency
        for (auto n : nums)
        {
            frequency[n]++;
        }
        for (auto [num, freq] : frequency)
        {
            if (k > freq && k != 1)
            { // Consider two cases and update the k.
                k -= freq;
            }
            else
            {
                return num;
            }
        }
        return -1;
    }    
```

## Approach 2

Using min-heap

``` C++
    int findKthLargest(vector<int>& nums, int k) {
        std::priority_queue<int, std::vector<int>, std::greater<int>> q;

        for (auto n : nums)
        {
            q.push(n);
            if (q.size() > k)
            {  // Make sure there are only k numbers
                q.pop();
            }
        }

        return q.top();
    }
```





