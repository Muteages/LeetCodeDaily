# Sort the Jumbled Numbers

https://leetcode.com/problems/sort-the-jumbled-numbers

You are given a 0-indexed integer array mapping which represents the mapping rule of a shuffled decimal system. mapping[i] = j means digit i should be mapped to digit j in this system.

The mapped value of an integer is the new integer obtained by replacing each occurrence of digit i in the integer with mapping[i] for all 0 <= i <= 9.

You are also given another integer array nums. Return the array nums sorted in non-decreasing order based on the mapped values of its elements.

Notes:

Elements with the same mapped values should appear in the same relative order as in the input.
The elements of nums should only be sorted based on their mapped values and not be replaced by them.

## Approach 1

``` C++
    vector<int> sortJumbled(vector<int>& mapping, vector<int>& nums) {
        int n = nums.size();
        std::vector<std::pair<int, int>> m2n(n);
        for (int i = 0; i < n; i++)
        {
            int num = nums[i], mapped = 0, rem = 0, digit = 1;
            do
            { // In case the origin number is 0. Execute it one time first
                rem = mapping[num % 10]; // Get the last digit number
                mapped += rem * digit;
                num /= 10;
                digit *= 10;
            }
            while (num > 0);
            m2n[i] = {mapped, nums[i]};
        }
        std::sort(m2n.begin(), m2n.end(), [](const std::pair<int, int>& l, const std::pair<int, int>& r){
            return l.first < r.first;
        });
        for (int i = 0; i < n; i++)
        {
            nums[i] = m2n[i].second;
        }
        return nums;
    }
```

## Approach 2

``` C++
    int convert(std::vector<int>& mapping, int num)
    {
        int mapped = 0, rem = 0, digit = 1;
        do
        { // In case the origin number is 0. Execute it one time first
            rem = mapping[num % 10]; // Get the last digit number
            mapped += rem * digit;
            num /= 10;
            digit *= 10;
        }
        while (num > 0);
        return mapped;
    }

    vector<int> sortJumbled(vector<int>& mapping, vector<int>& nums) {
        std::sort(nums.begin(), nums.end(), [&](int l, int r){
            return convert(mapping, l) < convert(mapping, r);
        });
        return nums;
    }
```