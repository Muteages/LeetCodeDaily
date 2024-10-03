# Make Sum Divisible by P

https://leetcode.com/problems/make-sum-divisible-by-p


Given an array of positive integers nums, remove the smallest subarray (possibly empty) such that the sum of the remaining elements is divisible by p. It is not allowed to remove the whole array.

Return the length of the smallest subarray that you need to remove, or -1 if it's impossible.

A subarray is defined as a contiguous block of elements in the array.

 

## Approach 1

Brute force TLE for large cases

``` C++
    int minSubarray(vector<int>& nums, int p) {
        int n = nums.size();
        long long sum = std::accumulate(nums.begin(), nums.end(), 0LL);
        if (sum < p) return -1;
        else if (sum % p == 0) return 0;
        int ans = n;
        for (int l = 0; l < n; l++)
        {
            int r = l;
            long long curSum = sum;
            while (r < n && r - l + 1 < ans)
            {
                curSum -= nums[r];
                if (curSum % p == 0)
                {
                    break;
                }
                r++;
            }
            ans = std::min(ans, r - l + 1);
            if (ans == 1) return ans;
        }
        return ans == n ? -1 : ans;
    }
```

## Approach 2

``` C++
    int minSubarray(vector<int>& nums, int p) {
        int n = nums.size();
        int rem = 0;
        for (int num : nums)
        {
            rem = (rem + num) % p;
        }
        if (rem == 0) return 0;

        std::unordered_map<int, int> remPos; // Record the last remainder seen position
        remPos[0] = -1;
        int curRem = 0, ans = n;
        for (int i = 0; i < n; i++)
        {
            curRem = (curRem + nums[i]) % p;
            int r = (curRem - rem + p) % p;
            if (remPos.count(r))
            {
                ans = std::min(ans, i - remPos[r]);
            }
            remPos[curRem] = i;
        }
        return ans == n ? -1 : ans;
    }
```