# Missing Number

https://leetcode.com/problems/missing-number

Given an array nums containing n distinct numbers in the range [0, n], return the only number in the range that is missing from the array.


## Approach 1
Sum 

``` C++
    int missingNumber(vector<int>& nums) {
        int realSum = std::accumulate(nums.begin(), nums.end(), 0);
        int n = nums.size();
        int sum = n * (n + 1) / 2;
        return sum - realSum;
    }
```

## Approach 2

XOR bit manipulation

``` C++
    int missingNumber(vector<int>& nums) {
        int ans = 0;
        int n = nums.size();
        for (int i = 0; i < n; i++)
        {
            ans ^= i;
            ans ^= nums[i];
        }
        ans ^= n;
        return ans;
    }
```


## Approach 2

Sort and check each number

``` C++
    int missingNumber(vector<int>& nums) {
        std::sort(nums.begin(), nums.end());
        for (int i = 0; i < nums.size(); i++)
        {
            if (i != nums[i])
            {
                return i;
            }
        }
        return nums.size();
    }
```

## Approach 3

SC: O(1) while TC O(n)
``` C++
    int missingNumber(vector<int>& nums) {
        std::vector<bool> visited(10001, false);
        for (int num : nums)
        {
            visited[num] = true;
        }
        int n = nums.size();
        for (int i = 0; i < n; i++)
        {
            if (!visited[i])
            {
                return i;
            }
        }
        return n;
    }
```

## Approach 4

Binary search
``` C++
    int missingNumber(vector<int>& nums) {
        std::sort(nums.begin(), nums.end());
        int n = nums.size();
        if (nums.back() < n)
        {
            return n;
        }
        int left = 0, right = n - 1;
        while (left <= right)
        {
            int mid = left + (right - left) / 2;
            if (nums[mid] == mid)
            {
                left = mid + 1;
            }
            else
            {
                right = mid - 1;
            }
        }
        return left;
    }
```