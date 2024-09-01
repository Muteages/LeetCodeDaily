# Convert 1D Array into 2D Array

https://leetcode.com/problems/convert-1d-array-into-2d-array


## Approach 1

``` C++
    vector<vector<int>> construct2DArray(vector<int>& original, int m, int n) {
        if (m * n != original.size()) return {};
        std::vector<std::vector<int>> ans(m);
        for (int i = 0; i < m; i++)
        {
            ans[i].assign(original.begin() + i * n, original.begin() + (i + 1) * n);
        }
        return ans;
    }
```

## Approach 2

``` JavaScript
var construct2DArray = function(original, m, n) {
    if (m * n !== original.length) return [];
    const ans = Array.from({length: m}, () => Array(n));
    let idx = 0;
    for (let col = 0; col < n; col++) {
        for (let row = 0; row < m; row++) {
            ans[row][col] = original[row * n + idx];
        }
        idx++;
    }
    return ans;
};
```