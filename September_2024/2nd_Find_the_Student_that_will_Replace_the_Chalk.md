# Find the Student that will Replace the Chalk

https://leetcode.com/problems/find-the-student-that-will-replace-the-chalk

There are n students in a class numbered from 0 to n - 1. The teacher will give each student a problem starting with the student number 0, then the student number 1, and so on until the teacher reaches the student number n - 1. After that, the teacher will restart the process, starting with the student number 0 again.

You are given a 0-indexed integer array chalk and an integer k. There are initially k pieces of chalk. When the student number i is given a problem to solve, they will use chalk[i] pieces of chalk to solve that problem. However, if the current number of chalk pieces is strictly less than chalk[i], then the student number i will be asked to replace the chalk.

Return the index of the student that will replace the chalk pieces.

## Approach 1

``` C++
    int chalkReplacer(vector<int>& chalk, int k) {
        long long total = std::accumulate(chalk.begin(), chalk.end(), 0LL);
        k %= total;
        for (int i = 0; i < chalk.size(); i++)
        {
            if (k < chalk[i])
            {
                return i;
            }
            k -= chalk[i];
        }
        return -1;
    }
```

## Approach 2

Use prefix and binary search to find the index more efficiently.

``` JavaScript
const binarySearch = (prefix, k) => {
    let l = 0, r = prefix.length - 1;
    while (l <= r) {
        let m = Math.floor((l + r) / 2);
        if (prefix[m] === k) {
            return m + 1;
        }
        else if (prefix[m] < k) {
            l = m + 1;
        }
        else {
            r = m - 1;
        }
    }
    return l;
};
var chalkReplacer = function(chalk, k) {
    const n = chalk.length;
    const prefix = Array(n).fill(chalk[0]);
    for (let i = 1; i <= n; i++) {
        prefix[i] = prefix[i - 1] + chalk[i];
    }
    k %= prefix[n - 1];
    
    return binarySearch(prefix, k);
};
```