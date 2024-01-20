# Sum of Subarray Minimums

https://leetcode.com/problems/sum-of-subarray-minimums

Given an array of integers arr, find the sum of min(b), where b ranges over every (contiguous) subarray of arr. Since the answer may be large, return the answer modulo 109 + 7.


## Approach 1

Brute force, TLE for large cases

``` C++
    int sumSubarrayMins(vector<int>& arr) {
        const int mod = 1e9 + 7;
        int ans = 0;
        int curSubLen = 1;
        while (curSubLen <= arr.size())
        {
            for (int i = 0; i <= arr.size() - curSubLen; i++)
            {
                int curMin = arr[i];
                for (int j = i + 1; j < i + curSubLen; j++)
                { // Find the minimum integer in current subarray
                    curMin = std::min(arr[j], curMin);
                }
                ans = (ans + curMin) % mod;
            }
            curSubLen++;
        }
        return ans;
    }
```

## Approach 2

``` C++
    int sumSubarrayMins(vector<int>& arr) {
        const int mod = 1e9 + 7;
        int n = arr.size();

        std::vector<int64_t> dp(n, -1);
        std::stack<int> st;
        int ans = 0;

        for (int i = 0; i < n; i++)
        {
            while (!st.empty() && arr[i] <= arr[st.top()])
            { // Find a proper range where the ith element is the minimum one 
                st.pop();
            }
            
            if (!st.empty())
            {
                dp[i] = dp[st.top()] + arr[i] * (i - st.top());
            }
            dp[i] = arr[i] * (i + 1);
            
            st.emplace(i);
            ans = (ans + dp[i]) % mod;
        }
        return ans;
```