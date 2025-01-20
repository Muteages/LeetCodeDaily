# First Completely Painted Row or Column

https://leetcode.com/problems/first-completely-painted-row-or-column

## Approach 

``` C++
    int firstCompleteIndex(vector<int>& arr, vector<vector<int>>& mat) {
        const int m = mat.size(), n = mat[0].size(), total = m * n;
        std::vector<std::pair<int, int>> mapping(total + 1);
        std::vector<int> rowRem(m, n), colRem(n, m);
        
        for (int r = 0; r < m; r++)
        {
            for (int c = 0; c < n; c++)
            {
                mapping[mat[r][c]] = {r, c};
            }
        }

        for (int i = 0; i < total; i++)
        {
            auto [r, c] = mapping[arr[i]];
            if (--rowRem[r] == 0 || --colRem[c] == 0)
            {
                return i;
            }
        }
        return -1;
    }
```

``` Python
    def firstCompleteIndex(self, arr: List[int], mat: List[List[int]]) -> int:
        m, n = len(mat), len(mat[0])
        total = m * n

        mapping = [(0, 0) for _ in range(total + 1)]
        rowRem = [n] * m
        colRem = [m] * n

        for r in range(m):
            for c in range(n):
                mapping[mat[r][c]] = (r, c)
        

        for i in range(total):
            (r, c) = mapping[arr[i]]
            rowRem[r] -= 1
            colRem[c] -= 1
            if rowRem[r] == 0 or colRem[c] == 0:
                return i
        
        return -1
```