# Arithmetic Subarrays

https://leetcode.com/problems/arithmetic-subarrays

A sequence of numbers is called arithmetic if it consists of at least two elements, and the difference between every two consecutive elements is the same. More formally, a sequence s is arithmetic if and only if s[i+1] - s[i] == s[1] - s[0] for all valid i.

You are given an array of n integers, nums, and two arrays of m integers each, l and r, representing the m range queries, where the ith query is the range [l[i], r[i]]. All the arrays are 0-indexed.

Return a list of boolean elements answer, where answer[i] is true if the subarray nums[l[i]], nums[l[i]+1], ... , nums[r[i]] can be rearranged to form an arithmetic sequence, and false otherwise.



## Approach 1

``` C++
    vector<bool> checkArithmeticSubarrays(vector<int>& nums, vector<int>& l, vector<int>& r) {
        int n = l.size();
        std::vector<bool> ans(n, false);
        for (int query = 0; query < n; query++)
        {
            int left = l[query], right = r[query];
            std::vector<int> temp(nums.begin() + left, nums.begin() + right + 1); // Creat sub-array
            std::sort(temp.begin(), temp.end());
            int diff = temp[1] - temp[0];
            bool flag = true;
            for (int i = 2; i < temp.size(); i++)
            { // Check if it's arithmetic
                if (temp[i] - temp[i - 1] != diff)
                { 
                    flag = false;
                    break;
                }
            }
            ans[query] = flag;
        }
        return ans;
    }
```

## Approach 2

Without sort

``` C++
    bool isArithmetic(std::vector<int>& nums, int l, int r)
    {
        std::unordered_set<int> us;
        int curMin = INT_MAX;
        int curMax = INT_MIN;

        for (int i = l; i <= r; i++)
        {
            curMin = std::min(curMin, nums[i]);
            curMax = std::max(curMax, nums[i]);
            us.insert(nums[i]);
        }

        int size = r - l + 1;
        if ((curMax - curMin) % (size - 1) != 0)
        { // Not arithmetic
            return false;
        }

        int diff = (curMax - curMin) / (size - 1);
        while (curMin < curMax)
        {
            curMin += diff;
            if (!us.count(curMin))
            {
                return false;
            }
        }
        return true;
    }
    vector<bool> checkArithmeticSubarrays(vector<int>& nums, vector<int>& l, vector<int>& r) {
        int n = l.size();
        std::vector<bool> ans(n, false);

        for (int i = 0; i < n; i++)
        {
            ans[i] = isArithmetic(nums, l[i], r[i]);
        }
        return ans;
    }
```

## Approach 3

``` C++
    bool isArithmetic(std::vector<int>& nums, int l, int r)
    {
        int curMin = INT_MAX;
        int curMax = INT_MIN;

        for (int i = l; i <= r; i++)
        {
            curMin = std::min(curMin, nums[i]);
            curMax = std::max(curMax, nums[i]);
        }

        int n = r - l + 1;
        if ((curMax - curMin) % (n - 1) != 0)
        {
            return false;
        }

        int diff = (curMax - curMin) / (n - 1);
        if (diff == 0)
        {
            return true;
        }
        std::vector<bool> vis(n, false);

        for (int i = l; i <= r; i++)
        {
            int curr = nums[i];
            if ((curr - curMin) % diff != 0)
            { // Not arithmetic
                return false;
            }
            else
            {
                int pos = (curr - curMin) / diff;
                if (vis[pos])
                { // Has a duplicate
                    return false;
                } 
                vis[pos] = true;
            }
        }
        return true;
    }
    vector<bool> checkArithmeticSubarrays(vector<int>& nums, vector<int>& l, vector<int>& r) {
        int n = l.size();
        std::vector<bool> ans(n, false);
        for (int i = 0; i < n; i++)
        {
            ans[i] = isArithmetic(nums, l[i], r[i]);
        }
        return ans;
    }
```