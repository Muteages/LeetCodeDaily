# Max Dot Product of Two Subsequences

https://leetcode.com/problems/max-dot-product-of-two-subsequences

Given two arrays nums1 and nums2.

Return the maximum dot product between non-empty subsequences of nums1 and nums2 with the same length.

## Approach 

``` C++
    int maxDotProduct(vector<int>& nums1, vector<int>& nums2) {

        int m = nums1.size();
        int n = nums2.size();
        std::vector<std::vector<int>> dp(m + 1, std::vector<int>(n + 1, INT_MIN));

        for(int i = 1; i <= m; i++)
        {
            for (int j = 1; j <= n; j++)
            {
                int current = nums1[i - 1] * nums2[j - 1];
                dp[i][j] = std::max({current + std::max(dp[i - 1][j - 1], 0), dp[i - 1][j], dp[i][j - 1]});
            }
        }
        return dp[m][n];
    }
```