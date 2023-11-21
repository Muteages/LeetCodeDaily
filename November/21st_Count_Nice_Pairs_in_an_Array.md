# Count Nice Pairs in an Array

https://leetcode.com/problems/count-nice-pairs-in-an-array

You are given an array nums that consists of non-negative integers. Let us define rev(x) as the reverse of the non-negative integer x. For example, rev(123) = 321, and rev(120) = 21. A pair of indices (i, j) is nice if it satisfies all of the following conditions:

0 <= i < j < nums.length
nums[i] + rev(nums[j]) == nums[j] + rev(nums[i])
Return the number of nice pairs of indices. Since that number can be too large, return it modulo 109 + 7.


## Approach 1

Brute force. Failed large cases

``` C++
    int rev(int num)
    {
        /*
            int r = 0;
            while (num)
            {
                r = r * 10 + num % 10;
                num /= 10;
            }
            return r;
        */
        std::string s = std::to_string(num);
        std::reverse(s.begin(), s.end());
        return std::stoi(s);
    }
    int countNicePairs(vector<int>& nums) {
        constexpr int mod = 1e9 + 7;
        int n = nums.size();
        int ans = 0;
        std::vector<int> reverseNums(n);
        for (int i = 0; i < n; i++)
        {
            reverseNums[i] = rev(nums[i]);
        }
        for (int i = 0; i < n - 1; i++)
        {
            for (int j = i + 1; j < n; j++)
            {
                if (nums[i] + reverseNums[j] == reverseNums[i] + nums[j])
                {
                    ans = (ans + 1) % mod;
                }
            }
        }
        return ans;
    }
```

## Approach 2

Count the frequency

``` C++
    int rev(int num)
    {
        std::string s = std::to_string(num);
        std::reverse(s.begin(), s.end());
        return std::stoi(s);
    }
    int countNicePairs(vector<int>& nums) {
        constexpr int mod = 1e9 + 7;
        int n = nums.size();
        int ans = 0;
        std::unordered_map<int, int> freq;
        // i + rev(j) = rev(i) + j ==> i - rev(i) = j - rev(j)
        for (int i = 0; i < n; i++)
        {
            nums[i] -= rev(nums[i]);
            freq[nums[i]]++;
            // ans = (ans + freq[nums[i]] - 1) % mod;  // Get the ans directly
        }

        for (auto [diff, f] : freq)
        {
            if (f > 1)
            {
                int sum = ((size_t)f * (f - 1) / 2) % mod;
                ans = (ans + sum) % mod;
            }
        }
        return ans;
    }
```