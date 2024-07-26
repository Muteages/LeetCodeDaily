# Find the City with the Smallest Number of Neighbours at a Threshold Distance

https://leetcode.com/problems/find-the-city-with-the-smallest-number-of-neighbors-at-a-threshold-distance

There are n cities numbered from 0 to n-1. Given the array edges where edges[i] = [fromi, toi, weighti] represents a bidirectional and weighted edge between cities fromi and toi, and given the integer distanceThreshold.

Return the city with the smallest number of cities that are reachable through some path and whose distance is at most distanceThreshold, If there are multiple such cities, return the city with the greatest number.

Notice that the distance of a path connecting cities i and j is equal to the sum of the edges' weights along that path.


## Approach 

Floyd Warshall Alog

``` C++
    void initMat(const std::vector<std::vector<int>>& edges, std::vector<std::vector<int>>& dp, int n, int threshold)
    {
        int u{}, v{}, weight{};
        for (auto& edge : edges)
        {
            u = edge[0], v = edge[1], weight = edge[2];
            if (weight <= threshold)
            {
                dp[u][v] = dp[v][u] = weight;
            }
        }

        for (int mid = 0; mid < n; mid++)
        {
            for (int st = 0; st < n; st++)
            {
                for (int end = 0; end < n; end++)
                {
                    if (st == end) continue;
                    dp[st][end] = std::min(dp[st][end], dp[st][mid] + dp[mid][end]);
                }
            }
        }
    }

    int findTheCity(int n, vector<vector<int>>& edges, int distanceThreshold) {
        std::vector<std::vector<int>> dp(n, std::vector<int>(n, 10001));
        initMat(edges, dp, n, distanceThreshold);
        int minPaths = n, ans = -1;
        for (int i = 0; i < n; i++)
        {
            int cnt = 0;
            for (int j = 0; j < n; j++)
            {
                cnt += (dp[i][j] <= distanceThreshold);
            }
            if (cnt <= minPaths)
            {
                minPaths = cnt;
                ans = i;
            }
        }
        return ans;
    }
```

``` JavaScript
var findTheCity = function(n, edges, distanceThreshold) {
    const dp = Array.from({length: n}, () => Array(n).fill(Infinity));
    const init = () => {
        for (let edge of edges) {
            let u = edge[0], v = edge[1], weight = edge[2];
            if (weight <= distanceThreshold) {
                dp[u][v] = weight;
                dp[v][u] = weight;
            }
        }

        for (let mid = 0; mid < n; mid++) {
            for (let st = 0; st < n; st++) {
                for (let end = 0; end < n; end++) {
                    if (st === end) continue;
                    dp[st][end] = Math.min(dp[st][end], dp[st][mid] + dp[mid][end]);
                }
            }
        }
    };
    
    init();
    let minPaths = n, ans = -1;
    for (let i = 0; i < n; i++) {
        let paths = 0;
        for (let j = 0; j < n; j++) {
            paths += (dp[i][j] <= distanceThreshold);
        }
        if (paths <= minPaths) {
            minPaths = paths;
            ans = i;
        }
    }
    return ans;
};
```