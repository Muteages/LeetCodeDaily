# Maximum Product of Two Elements in an Array

Given the array of integers nums, you will choose two different indices i and j of that array. Return the maximum value of (nums[i]-1)*(nums[j]-1).

## Approach 1
Sort function
``` C++
    int maxProduct(vector<int>& nums) {
        std::sort(nums.begin(), nums.end());
        int i = nums[nums.size() - 2] - 1;
        int j = nums.back() - 1;
        return i * j;
    }
```

## Approach 2
Find the biggest and second biggest elements

``` C++
    int maxProduct(vector<int>& nums) {
        int i{}; // The biggest element
        int j{}; // Second biggest element
        for (int num : nums)
        {
            if (num > i)
            {
                j = i;
                i = num;
            }
            else if (num > j)
            {
                j = num;
            }
        }
        return (i - 1) * (j - 1);
    }
```