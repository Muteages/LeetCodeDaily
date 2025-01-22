# Map of Highest Peak

https://leetcode.com/problems/map-of-highest-peak

You are given an integer matrix isWater of size m x n that represents a map of land and water cells.

If isWater[i][j] == 0, cell (i, j) is a land cell.
If isWater[i][j] == 1, cell (i, j) is a water cell.
You must assign each cell a height in a way that follows these rules:

The height of each cell must be non-negative.
If the cell is a water cell, its height must be 0.
Any two adjacent cells must have an absolute height difference of at most 1. A cell is adjacent to another cell if the former is directly north, east, south, or west of the latter (i.e., their sides are touching).
Find an assignment of heights such that the maximum height in the matrix is maximized.

Return an integer matrix height of size m x n where height[i][j] is cell (i, j)'s height. If there are multiple solutions, return any of them.

## Approach 

Multi-source bfs
``` C++
    vector<vector<int>> highestPeak(vector<vector<int>>& isWater) {
        const int m = isWater.size(), n = isWater[0].size();
        const std::vector<std::pair<int, int>> dir = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};
        std::vector<std::vector<int>> ans(m, std::vector<int>(n, -1));

        std::queue<std::pair<int, int>> bfs;
        for (int r = 0; r < m; r++)
        {
            for (int c = 0; c < n; c++)
            {
                if (isWater[r][c])
                { // Fill all water cells into the queue first
                    bfs.emplace(r, c);
                    ans[r][c] = 0;
                }
            }
        }

        while (!bfs.empty())
        {
            auto [r, c] = bfs.front();
            bfs.pop();

            for (auto [dr, dc] : dir)
            {
                int nr = r + dr, nc = c + dc;
                if (nr >= 0 && nr < m && nc >= 0 && nc < n && ans[nr][nc] == -1)
                { // If next adjacent cell is valid and has not been visited, update its height and add it into the queue
                    ans[nr][nc] = ans[r][c] + 1;
                    bfs.emplace(nr, nc);
                }
            }
        }
        return ans;
    }
```

``` Python
    def highestPeak(self, isWater: List[List[int]]) -> List[List[int]]:
        m, n = len(isWater), len(isWater[0])
        dir = [[0, 1], [0, -1], [1, 0], [-1, 0]]
        ans = [[-1] * n for _ in range(m)]

        q = deque()
        for r, row in enumerate(isWater):
            for c, is_water in enumerate(row):
                if is_water:
                    ans[r][c] = 0
                    q.append((r, c))
        
        while q:
            r, c = q.popleft()

            for dr, dc in dir:
                nr, nc = r + dr, c + dc
                if nr >= 0 and nr < m and nc >= 0 and nc < n and ans[nr][nc] == -1:
                    ans[nr][nc] = ans[r][c] + 1
                    q.append((nr, nc))
        
        return ans
```

``` JavaScript
var highestPeak = function(isWater) {
    const m = isWater.length, n = isWater[0].length;
    const dir = [[0, 1], [0, -1], [1, 0], [-1, 0]];
    
    const ans = Array.from({length: m}, () => Array(n).fill(-1));
    const q = [];

    for (let r = 0; r < m; r++) {
        for (let c = 0; c < n; c++) {
            if (isWater[r][c] === 1) {
                q.push([r, c]);
                ans[r][c] = 0;
            }
        }
    }
    let front = 0; // Avoid TLE
    while (front < q.length) {
        const [r, c] = q[front++];
        for (const [dr, dc] of dir) {
            let nr = r + dr, nc = c + dc;
            if (nr >= 0 && nr < m && nc >= 0 && nc < n && ans[nr][nc] === -1) {
                q.push([nr, nc]);
                ans[nr][nc] = ans[r][c] + 1;
            }
        }
    }
    return ans;
};
```