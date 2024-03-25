# Find the Duplicate Number

https://leetcode.com/problems/find-the-duplicate-number

Given an array of integers nums containing n + 1 integers where each integer is in the range [1, n] inclusive.

There is only one repeated number in nums, return this repeated number.


## Approach 1

``` C++
    int findDuplicate(vector<int>& nums) {
        std::unordered_set<int> unique;
        for (int num : nums)
        {
            if (unique.count(num))
            {
                return num;
            }
            unique.insert(num);
        }
        return -1;
    }
```

## Approach 2

``` C++
    int findDuplicate(vector<int>& nums) {
        int left = 1;
        int right = nums.size() - 1;

        while (left < right)
        {
            int mid = left + (right - left) / 2;
            int cnt = 0;
            for (const int& num : nums)
            {
                cnt += (num <= mid);
            }
            if (cnt > mid)
            { // Which means the duplicates lie in the left half side
                right = mid;
            }
            else
            {
                left = mid + 1;
            }
        }
        return left;
    }
```

## Approach 3

Tortoise and Hare algorithm

``` C++
    int findDuplicate(vector<int>& nums) {
        int slow = nums[0];
        int fast = nums[0];

        // Find the intersection number
        do
        {
            slow = nums[slow];
            fast = nums[nums[fast]];
        }
        while (slow != fast);

        slow = nums[0];
        while (slow != fast)
        { // Find the entrance of the cycle, i.e the duplicate number
            slow = nums[slow];
            fast = nums[fast];
        }

        return slow;
    }
```

 