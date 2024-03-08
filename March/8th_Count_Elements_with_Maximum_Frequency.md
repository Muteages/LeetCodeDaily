# Count Elements with Maximum Frequency

https://leetcode.com/problems/count-elements-with-maximum-frequency

You are given an array nums consisting of positive integers.

Return the total frequencies of elements in nums such that those elements all have the maximum frequency.

The frequency of an element is the number of occurrences of that element in the array.

## Approach 1

``` C++
    int maxFrequencyElements(vector<int>& nums) {
        std::vector<int> freq(101, 0);
        int maxFreq = 0, cnt = 0;
        for (int num : nums)
        {
            freq[num]++;
            cnt += freq[num] == maxFreq;
            if (freq[num] > maxFreq)
            {
                cnt = 1;
                maxFreq = freq[num];
            }
        }
        return cnt * maxFreq;
    }

```

## Approach 2

``` C++
    int maxFrequencyElements(vector<int>& nums) {
        std::vector<int> freq(101, 0);
        for (int num : nums)
        {
            freq[num]++;
        }

        std::sort(freq.rbegin(), freq.rend());
        for (int i = 1; i < 101; i++)
        {
            if (freq[i] != freq[i - 1])
            {
                return freq[i - 1] * i;
            }
        }
        return -1;
    }
```