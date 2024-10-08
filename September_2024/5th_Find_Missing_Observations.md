# Find Missing Observations

https://leetcode.com/problems/find-missing-observations


You have observations of n + m 6-sided dice rolls with each face numbered from 1 to 6. n of the observations went missing, and you only have the observations of m rolls. Fortunately, you have also calculated the average value of the n + m rolls.

You are given an integer array rolls of length m where rolls[i] is the value of the ith observation. You are also given the two integers mean and n.

Return an array of length n containing the missing observations such that the average value of the n + m rolls is exactly mean. If there are multiple valid answers, return any of them. If no such array exists, return an empty array.

The average value of a set of k numbers is the sum of the numbers divided by k.

Note that mean is an integer, so the sum of the n + m rolls should be divisible by n + m.

## Approach 

``` C++
    vector<int> missingRolls(vector<int>& rolls, int mean, int n) {
        int m = rolls.size();
        int subSum = std::accumulate(rolls.begin(), rolls.end(), 0);
        int rem = mean * (m + n) - subSum;
        if (rem > 6 * n || rem < n)
        { // It's impossible to allocate dices
            return {};
        }

        int base = rem / n;
        rem %= n;
        std::vector<int> ans(n, base);
        for (int i = 0; i < rem; i++)
        {
            ans[i]++;
        }
        return ans;
    }
```

``` JavaScript
var missingRolls = function(rolls, mean, n) {
    let subSum = rolls.reduce((acc, val) => acc + val, 0);
    let m = rolls.length;
    let rem = mean * (m + n) - subSum;

    if (rem < n || rem > n * 6) return [];

    let base = Math.floor(rem / n);
    rem %= n;
    let ans = Array(n).fill(base);
    for (let i = 0; i < rem; i++) {
        ans[i]++;
    }
    return ans;
};
```