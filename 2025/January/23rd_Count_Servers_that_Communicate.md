# Count Servers that Communicate

https://leetcode.com/problems/count-servers-that-communicate

You are given a map of a server center, represented as a m * n integer matrix grid, where 1 means that on that cell there is a server and 0 means that it is no server. Two servers are said to communicate if they are on the same row or on the same column.

Return the number of servers that communicate with any other server.


## Approach 

``` C++
    int countServers(vector<vector<int>>& grid) {
        int m = grid.size(), n = grid[0].size();

        std::vector<int> rows(m, 0), cols(n, 0);
        for (int r = 0; r < m; r++)
        {
            for (int c = 0; c < n; c++)
            {
                if (grid[r][c] == 1)
                {
                    rows[r]++;
                    cols[c]++;
                }
            }
        }
        int ans = 0;
        for (int r = 0; r < m; r++)
        {
            for (int c = 0; c < n; c++)
            {
                if (grid[r][c] == 1 && (rows[r] > 1 || cols[c] > 1))
                {
                    ans++;
                }
            }
        }
        return ans;
    }
```

``` Python
    def countServers(self, grid: List[List[int]]) -> int:
        m, n = len(grid), len(grid[0])
        rows = [sum(row) for row in grid]
        cols = [sum(col) for col in zip(*grid)]
        
        ans = 0
        for r in range(m):
            for c in range(n):
                if grid[r][c] == 1 and (rows[r] > 1 or cols[c] > 1):
                    ans += 1
        
        return ans
```

``` JavaScript
    const rows = grid.map(row => row.reduce((acc, val) => acc + val, 0));
    const cols = grid[0].map((_, colIdx) => grid.reduce((acc, row) => acc + row[colIdx], 0));

    return grid.reduce((ans, row, r) =>
        ans + row.reduce((acc, isServer, c) =>
            acc + (isServer && (rows[r] > 1 || cols[c] > 1)), 0), 0);
```