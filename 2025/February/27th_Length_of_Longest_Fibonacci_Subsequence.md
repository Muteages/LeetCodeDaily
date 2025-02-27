# Length of Longest Fibonacci Subsequence

https://leetcode.com/problems/length-of-longest-fibonacci-subsequence

A sequence x1, x2, ..., xn is Fibonacci-like if:

n >= 3
xi + xi+1 == xi+2 for all i + 2 <= n
Given a strictly increasing array arr of positive integers forming a sequence, return the length of the longest Fibonacci-like subsequence of arr. If one does not exist, return 0.

A subsequence is derived from another sequence arr by deleting any number of elements (including none) from arr, without changing the order of the remaining elements. For example, [3, 5, 8] is a subsequence of [3, 4, 5, 6, 7, 8].


## Approach 

``` C++
    int lenLongestFibSubseq(vector<int>& arr) {
        std::unordered_map<int, int> n2i;
        const int n = arr.size();
        for (int i = 0; i < n; i++)
        {
            n2i[arr[i]] = i;
        }

        std::vector<std::vector<int>> dp(1000, std::vector<int>(1000, 2));
        int ans = 0;
        for (int j = 1; j < n - 1; j++)
        {   
            for (int k = j + 1; k < n; k++)
            {
                int iv = arr[k] - arr[j]; // arr[i]
                if (iv < arr[j] && n2i.count(iv))
                {
                    int i = n2i[iv];
                    dp[j][k] = dp[i][j] + 1;
                }
                ans = std::max(ans, dp[j][k]);
            }
        }
        return ans > 2 ? ans : 0;
    }
```


``` Python
    def lenLongestFibSubseq(self, arr: List[int]) -> int:
        ans = 0
        n = len(arr)
        v2i = defaultdict(int) # val - index
        dp = [[2] * n for _ in range(n)]
        for k, v in enumerate(arr):
            v2i[v] = k
            for j in range(k - 1, -1, -1):
                i_val = arr[k] - arr[j]
                if i_val < arr[j] and i_val in v2i:
                    i = v2i[i_val]
                    dp[j][k] = dp[i][j] + 1
                ans = max(ans, dp[j][k])
        return ans if ans > 2 else 0
```

Brute Froce, Just a practice
``` JavaScript
var lenLongestFibSubseq = function(arr) {
    s = new Set(arr);
    const n = arr.length;
    ans = 0;
    for (i = 0; i < n - 2; i++) {
        for (j = i + 1; j < n - 1; j++) {
            let vi = arr[i], vj = arr[j];
            let len = 3;
            for (; s.has(vi + vj); len++) {
                [vi, vj] = [vj, vi + vj];
            }
            ans = Math.max(ans, len - 1);
        }
    }
    return ans > 2 ? ans : 0;
};
```