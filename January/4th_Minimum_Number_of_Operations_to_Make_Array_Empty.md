# Minimum Number of Operations to Make Array Empty

https://leetcode.com/problems/minimum-number-of-operations-to-make-array-empty

You are given a 0-indexed array nums consisting of positive integers.

There are two types of operations that you can apply on the array any number of times:

Choose two elements with equal values and delete them from the array.
Choose three elements with equal values and delete them from the array.
Return the minimum number of operations required to make the array empty, or -1 if it is not possible.


## Approach 

``` C++
    int minOperations(vector<int>& nums) {
        std::unordered_map<int, int> freq;
        for (const int& num : nums)
        {
            freq[num]++;
        }

        int ans = 0;
        for (const auto& [num, f] : freq)
        {
            if (f == 1)
            { // Unable to apply op1 or op2
                return -1;
            }
            else if (f % 3 == 0)
            { // Only apply op2
                ans += f / 3;
            }
            else if (f % 3 == 1)
            { 
                ans += f / 3 - 1 + 2;
            }
            else 
            {
                ans += f / 3 + (f % 3) / 2;
            }

        }
        return ans;
    }
```

## Revised

``` C++
    int minOperations(vector<int>& nums) {
        std::unordered_map<int, int> freq;
        for (const int& num : nums)
        {
            freq[num]++;
        }

        int ans = 0;
        for (const auto& [num, f] : freq)
        {
            if (f == 1)
            { // Unable to apply op1 or op2
                return -1;
            }
            
            auto [op2, rem] = std::div(f, 3);
            ans += op2 + (rem != 0); 
        }
        return ans;
    }
```