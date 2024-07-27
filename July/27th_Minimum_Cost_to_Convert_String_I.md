# Minimum Cost to Convert String


https://leetcode.com/problems/minimum-cost-to-convert-string-i

You are given two 0-indexed strings source and target, both of length n and consisting of lowercase English letters. You are also given two 0-indexed character arrays original and changed, and an integer array cost, where cost[i] represents the cost of changing the character original[i] to the character changed[i].

You start with the string source. In one operation, you can pick a character x from the string and change it to the character y at a cost of z if there exists any index j such that cost[j] == z, original[j] == x, and changed[j] == y.

Return the minimum cost to convert the string source to the string target using any number of operations. If it is impossible to convert source to target, return -1.

Note that there may exist indices i, j such that original[j] == original[i] and changed[j] == changed[i].

## Approach 

Floyd Warshall

``` C++
    void init(const std::vector<char>& original, 
              const std::vector<char>& changed, 
              const std::vector<int>& cost,
              std::vector<std::vector<int>>& dp)
    {

        for (int i = 0; i < original.size(); i++)
        {
            char u = original[i], v = changed[i];
            int c = cost[i];
            dp[u - 'a'][v - 'a'] = std::min(dp[u - 'a'][v - 'a'], c);
        }
        for (int mid = 0; mid < 26; mid++)
        {
            for (int st = 0; st < 26; st++)
            {
                for (int end = 0; end < 26; end++)
                {
                    if (st == end) continue;
                    dp[st][end] = std::min((long long)dp[st][end], (long long)dp[st][mid] + dp[mid][end]);
                }
            }
        }
    }

    long long minimumCost(string source, string target, vector<char>& original, vector<char>& changed, vector<int>& cost) {

        std::vector<std::vector<int>> dp(26, std::vector<int>(26, INT_MAX));
        init(original, changed, cost, dp);
        long long ans = 0;
        for (int i = 0; i < source.size(); i++)
        {
            char s = source[i], t = target[i];
            if (s == t) continue;
            int c = dp[s - 'a'][t - 'a'];
            if (c == INT_MAX) return -1;
            ans += c;
        }
        return ans;
    }
```