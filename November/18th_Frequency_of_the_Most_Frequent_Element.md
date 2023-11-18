# Frequency of the Most Frequent Element

https://leetcode.com/problems/frequency-of-the-most-frequent-element

The frequency of an element is the number of times it occurs in an array.

You are given an integer array nums and an integer k. In one operation, you can choose an index of nums and increment the element at that index by 1.

Return the maximum possible frequency of an element after performing at most k operations.

## Approach 1

TLE for large cases
``` C++
    int maxFrequency(vector<int>& nums, int k) {
        std::sort(nums.begin(), nums.end());
        int ans = 1; // Because we have at least one selected element
        for (int pivot = 1; pivot < nums.size(); pivot++)
        {
            int tempCount = 1;
            int operations = k;
            int candidate = pivot - 1;
            while (candidate >= 0)
            {
                if (operations >= nums[pivot] - nums[candidate])
                { // It's possible to convert the current element to pivot element
                    operations -= nums[pivot] - nums[candidate];
                    tempCount++;
                    candidate--;
                }
                else
                { // Unable to convert
                    break;
                }
            }
            ans = std::max(ans, tempCount);
        }
        return ans;
    }
```

## Approach 2 

Sliding window

``` C++
    int maxFrequency(vector<int>& nums, int k) {
        std::sort(nums.begin(), nums.end());
        int ans = 0;
        long sum = 0;
        int left = 0;
        for (int right = 0; right < nums.size(); right++)
        {
            sum += nums[right];
            while ((long)(nums[right]) * (right - left + 1) > sum + k)
            { // Failed to cover current range, move the left to right 1 unit
                sum -= nums[left];
                left++;
            }
            ans = std::max(ans, right - left + 1);
        }
        return ans;
    }
```

## Approach 3

Use counting sort instead of built-in sort function
``` C++
    void countingSort(std::vector<int>& nums)
    {
        int maxNum = *std::max_element(nums.begin(), nums.end());
        std::vector<int> frequency(maxNum + 1, 0);
        for (auto num : nums)
        {
            frequency[num]++;
        }

        int index = 0;
        for (int i = 0; i <= maxNum; i++)
        {
            while (frequency[i])
            {
                nums[index] = i;
                index++;
                frequency[i]--;
            }
        }
    }
    int maxFrequency(vector<int>& nums, int k) {
        countingSort(nums);
        int ans = 0;
        long sum = 0;
        int left = 0;
        for (int right = 0; right < nums.size(); right++)
        {
            sum += nums[right];
            while ((long)(nums[right]) * (right - left + 1) > sum + k)
            { // Failed to cover the current range, move the left to right 1 unit
                sum -= nums[left];
                left++;
            }
            ans = std::max(ans, right - left + 1);
        }
        return ans;
    }
```