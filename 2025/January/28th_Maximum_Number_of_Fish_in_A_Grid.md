# Maximum Number of Fish in A Grid

https://leetcode.com/problems/maximum-number-of-fish-in-a-grid

You are given a 0-indexed 2D matrix grid of size m x n, where (r, c) represents:

A land cell if grid[r][c] = 0, or
A water cell containing grid[r][c] fish, if grid[r][c] > 0.
A fisher can start at any water cell (r, c) and can do the following operations any number of times:

Catch all the fish at cell (r, c), or
Move to any adjacent water cell.
Return the maximum number of fish the fisher can catch if he chooses his starting cell optimally, or 0 if no water cell exists.

An adjacent cell of the cell (r, c), is one of the cells (r, c + 1), (r, c - 1), (r + 1, c) or (r - 1, c) if it exists.

## Approach 

``` C++
    int m, n;
    int dfs(std::vector<std::vector<int>>& grid, int r, int c)
    {
        if (r < 0 || r >= m || c < 0 || c >= n || grid[r][c] == 0) return 0;

        int fish = grid[r][c];
        grid[r][c] = 0; // Mark as visited
        fish += dfs(grid, r - 1, c);
        fish += dfs(grid, r + 1, c);
        fish += dfs(grid, r, c - 1);
        fish += dfs(grid, r, c + 1);
        return fish;
    }


    int findMaxFish(vector<vector<int>>& grid) {
        m = grid.size(), n = grid[0].size();
        int ans = 0;
        for (int r = 0; r < m; r++)
        {
            for (int c = 0; c < n; c++)
            {
                if (grid[r][c] == 0) continue;
                int fish = dfs(grid, r, c);
                ans = std::max(ans, fish);
            }
        }
        return ans;
    }
```

``` Python
    def findMaxFish(self, grid: List[List[int]]) -> int:
        m, n = len(grid), len(grid[0])
        dir = [[0, 1], [0, -1], [1, 0], [-1, 0]]

        def dfs(r: int, c: int) -> int:
            if r < 0 or r >= m or c < 0 or c >= n or grid[r][c] == 0:
                return 0
            
            fish = grid[r][c]
            grid[r][c] = 0 # Mark as visited
            for dr, dc in dir:
                fish += dfs(r + dr, c + dc)
            
            return fish
        
        ans = 0
        for r in range(m):
            for c in range(n):
                if grid[r][c] != 0:
                    ans = max(ans, dfs(r, c))
        
        return ans
```

## Approach 2

BFS
``` C++
public:
    int m, n;
    int bfs(std::vector<std::vector<int>>& grid, int r, int c)
    {
        std::vector<std::pair<int, int>> dir = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};

        int fish = 0;
        std::queue<std::pair<int, int>> q{};
        q.emplace(r, c);
        while (!q.empty())
        {
            auto [cr, cc] = q.front();
            q.pop();
            fish += grid[cr][cc];
            grid[cr][cc] = 0;
            for (auto [dr, dc] : dir)
            {
                int nr = cr + dr, nc = cc + dc;
                if (nr >= 0 && nr < m && nc >= 0 && nc < n && grid[nr][nc] != 0)
                {
                    q.emplace(nr, nc);
                }
            }
        }
        return fish;
    }


    int findMaxFish(vector<vector<int>>& grid) {
        m = grid.size(), n = grid[0].size();
        int ans = 0;
        for (int r = 0; r < m; r++)
        {
            for (int c = 0; c < n; c++)
            {
                if (grid[r][c] == 0) continue;
                ans = std::max(ans, bfs(grid, r, c));
            }
        }
        return ans;
    }
```