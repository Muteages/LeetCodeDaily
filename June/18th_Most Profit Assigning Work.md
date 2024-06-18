# Most Profit Assigning Work

https://leetcode.com/problems/most-profit-assigning-work

You have n jobs and m workers. You are given three arrays: difficulty, profit, and worker where:

difficulty[i] and profit[i] are the difficulty and the profit of the ith job, and
worker[j] is the ability of jth worker (i.e., the jth worker can only complete a job with difficulty at most worker[j]).
Every worker can be assigned at most one job, but one job can be completed multiple times.

For example, if three workers attempt the same job that pays $1, then the total profit will be $3. If a worker cannot complete any job, their profit is $0.
Return the maximum profit we can achieve after assigning the workers to the jobs.



## Approach 1

``` C++
    int maxProfitAssignment(vector<int>& difficulty, vector<int>& profit, vector<int>& worker) {
        const int n = profit.size();
        std::vector<int> d2p(100001, 0); // index: difficulty - dp2[i] profit
        std::sort(worker.begin(), worker.end());
        for (int i = 0; i < n; ++i)
        {
            d2p[difficulty[i]] = std::max(d2p[difficulty[i]], profit[i]);
        }
        int ans = 0, curMaxProfit = 0, prevMaxDifficulty = 1;
        for (int w : worker)
        {
            for (; prevMaxDifficulty <= w; ++prevMaxDifficulty)
            {
                curMaxProfit = std::max(curMaxProfit, d2p[prevMaxDifficulty]);
            }
            ans += curMaxProfit;
        }
        return ans;
    }
```

## Approach 2

Optimal Approach

``` C++
    int maxProfitAssignment(vector<int>& difficulty, vector<int>& profit, vector<int>& worker) {
        const int n = profit.size();
        std::vector<int> d2p(100001, 0); // index: difficulty - dp2[i] profit
        int maxDifficulty = 0;
        std::sort(worker.begin(), worker.end());
        for (int i = 0; i < n; ++i)
        {
            d2p[difficulty[i]] = std::max(d2p[difficulty[i]], profit[i]);
            maxDifficulty = std::max(maxDifficulty, difficulty[i]);
        }

        for (int i = 1; i <= maxDifficulty; ++i)
        {
            d2p[i] = std::max(d2p[i], d2p[i - 1]);
        }
        d2p.resize(maxDifficulty + 1);
        int ans = 0;
        for (int w : worker)
        {
            ans += w > maxDifficulty ? d2p[maxDifficulty] : d2p[w];
        }
        return ans;
    }
```

``` JavaScript
var maxProfitAssignment = function(difficulty, profit, worker) {
    let maxDifficulty = Math.max(...difficulty);
    let d2p = new Array(maxDifficulty + 1).fill(0);
    for (let i = 0; i < profit.length; i++) {
        d2p[difficulty[i]] = Math.max(d2p[difficulty[i]], profit[i]);
    }
    for (let i = 1; i <= maxDifficulty; i++) {
        d2p[i] = Math.max(d2p[i], d2p[i - 1]);
    }

    let ans = 0;
    worker.forEach((w) => {
        ans += w > maxDifficulty ? d2p[maxDifficulty] : d2p[w];
    });
    return ans;
};
```