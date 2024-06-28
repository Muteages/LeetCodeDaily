# Maximum Total Importance of Roads

https://leetcode.com/problems/maximum-total-importance-of-roads

You are given an integer n denoting the number of cities in a country. The cities are numbered from 0 to n - 1.

You are also given a 2D integer array roads where roads[i] = [ai, bi] denotes that there exists a bidirectional road connecting cities ai and bi.

You need to assign each city with an integer value from 1 to n, where each value can only be used once. The importance of a road is then defined as the sum of the values of the two cities it connects.

Return the maximum total importance of all roads possible after assigning the values optimally.


## Approach 1
Greedy 

``` JavaScript
var maximumImportance = function(n, roads) {
    let deg = new Array(n).fill(0);
    roads.forEach((road) => {
        const [a, b] = road;
        deg[a]++;
        deg[b]++;
    });
    deg.sort((a, b) => a - b);
    let ans = 0;
    for (let imp = 1; imp <= n; imp++) {
        ans += imp * deg[imp - 1];
    }
    return ans;
};
```

## Approach 2

Without sorting. 

``` C++
    long long maximumImportance(int n, vector<vector<int>>& roads) {
        std::vector<int> deg(n, 0);
        int maxDeg = 0;
        for (const auto& road : roads)
        {
            maxDeg = std::max({maxDeg, ++deg[road[0]], ++deg[road[1]]});
        }

        std::vector<int> freq(maxDeg + 1, 0);
        for (int d : deg) 
        {
            freq[d]++;
        }

        long long ans = 0;
        int imp = n;
        for (int d = maxDeg; d > 0; d--) 
        {
            int k = freq[d];
            ans += (2LL * imp - k + 1) * k / 2 * d;
            imp -= k;
        }
        return ans;
    }
```


``` JavaScript
var maximumImportance = function(n, roads) {
    let deg = new Array(n).fill(0);
    let maxDeg = -1;
    roads.forEach((road) => {
        const [a, b] = road;
        deg[a]++;
        deg[b]++;
        maxDeg = Math.max(maxDeg, deg[a], deg[b]);
    });

    let degFreq = new Array(maxDeg + 1).fill(0);
    deg.forEach((d) => {
        degFreq[d]++;
    });

    let ans = 0, imp = n;
    for (let i = maxDeg; i > 0; i--) {
        let k = degFreq[i];
        ans += i * (2 * imp - k + 1) * k / 2;
        imp -= k;
    }
    return ans;
};
```
