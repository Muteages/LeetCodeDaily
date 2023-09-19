# Find the Duplicate Number

https://leetcode.com/problems/find-the-duplicate-number

Given an array of integers nums containing n + 1 integers where each integer is in the range [1, n] inclusive.

There is only one repeated number in nums, return this repeated number.

## Approach 1

Convert to the linked list cycle problem

``` C++
    int findDuplicate(vector<int>& nums) {
        int slow = nums[0];
        int fast = nums[0];

        do
        {   // Find the cycle 
            slow = nums[slow];
            fast = nums[nums[fast]];
        }
        while (slow != fast);

        // Reset
        slow = nums[0]; 
        while(slow != fast)
        { // Find the cycle start point, i.e the duplicate number
            slow = nums[slow];
            fast = nums[fast];
        }
        return slow;
    }
```

## Approach 2

Sort

``` C++
    int findDuplicate(vector<int>& nums) {
        std::sort(nums.begin(), nums.end());

        int i = 1;
        while (i < nums.size())
        {
            if (nums[i - 1] == nums[i])
            {
                return nums[i];
            }
            i++;
        }
        return -1;
    }
```

## Approach 3

Treat the number as a dummy index and visit all dummy indices.

``` C++
    int findDuplicate(vector<int>& nums) {
        for (int i = 0; i < nums.size(); i++)
        {
            int dummy = std::abs(nums[i]); // Treat the number as a dummy index

            nums[dummy] *= -1;
            if (nums[dummy] > 0)
            { // Only the duplicate index will be visited twice or more and hence only it will be positive
                return dummy;
            }
        }
        return -1;
    }
```

## Approach 4

Binary Search

``` C++
    int findDuplicate(vector<int>& nums) {
        int l = 0, r = nums.size() - 1;
        while (l <= r)
        {
            int m = l + (r - l) / 2;
            int sum = 0;
            for (const auto& n : nums)
            {
                if (n <= m)
                {
                    sum++;
                }
            }

            if (sum <= m)
            {
                l = m;
            }
            else 
            {
                r = m - 1;
            }
        }
        return l;
    }
```