# Sort by Parity

https://leetcode.com/problems/sort-array-by-parity/description

Given an integer array nums, move all the even integers at the beginning of the array followed by all the odd integers.

Return any array that satisfies this condition.

## Approach 1

Modify the vector in place

``` C++
    vector<int> sortArrayByParity(vector<int>& nums) {
        if (nums.size() == 1)
        {
            return nums;
        }
        int i = 0;
        int j = nums.size() - 1;
        while (i < j)
        {
            while (i < j && nums[i] % 2 == 0)
            { // Find the first even number from tail
                i++;
            }
            while (i < j && nums[j] % 2 != 0)
            { // Find the first odd number from head
                j--;
            }
            std::swap(nums[i], nums[j]);
            i++;
            j--;
        }
        return nums;
    }
```

## Approach 2

Use deque

``` C++
    vector<int> sortArrayByParity(vector<int>& nums) {
        if (nums.size() == 1)
        {
            return nums;
        }
        std::deque<int> ans;
        for (auto n : nums)
        {
            if (n % 2 == 1)
            {
                ans.push_back(n);
            }
            else
            {
                ans.push_front(n);
            }
        }
        return std::vector<int>(ans.begin(), ans.end());
    }
```

## Approach 3
``` C++
    vector<int> sortArrayByParity(vector<int>& nums) {
        if (nums.size() == 1)
        {
            return nums;
        }

        int i = 0;
        for (int j = 0; j < nums.size(); j++)
        {
            if (nums[j] % 2 == 0)
            {
                std::swap(nums[i], nums[j]);
                i++;
            }
        }
        return nums;
    }
```