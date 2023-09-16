# Path with Minimum Effort

https://leetcode.com/problems/path-with-minimum-effort/description

You are a hiker preparing for an upcoming hike. You are given heights, a 2D array of size rows x columns, where heights[row][col] represents the height of cell (row, col). You are situated in the top-left cell, (0, 0), and you hope to travel to the bottom-right cell, (rows-1, columns-1) (i.e., 0-indexed). You can move up, down, left, or right, and you wish to find a route that requires the minimum effort.

A route's effort is the maximum absolute difference in heights between two consecutive cells of the route.

Return the minimum effort required to travel from the top-left cell to the bottom-right cell.


## Approach 1 

Dijkstra Algorithm

``` C++
    int minimumEffortPath(vector<vector<int>>& heights) {
        int h = heights.size();
        int n = heights[0].size();

        std::vector<std::vector<int>> efforts(h, std::vector<int>(n, INT_MAX)); // Record the minimum effort to reach each cell.
        efforts[0][0] = 0;

        std::priority_queue<std::tuple<int, int, int>, std::vector<std::tuple<int, int, int>>, std::greater<>> pq; // effort, x, y
        pq.emplace(0, 0, 0); 

        std::vector<std::vector<int>> dirs{{0, 1}, {0, -1}, {1, 0}, {-1, 0}};

        while (!pq.empty())
        {
            auto [effort, x, y] = pq.top();
            pq.pop();

            if (effort <= efforts[x][y])
            {
                if (x == h - 1 && y == n - 1)
                {
                    return effort;
                }

                for (auto dir : dirs)
                {
                    int nx = x + dir[0];
                    int ny = y + dir[1];

                    if (nx >= 0 && nx < h && ny >= 0 && ny < n)
                    {
                        int eff = std::max(effort, std::abs(heights[nx][ny] - heights[x][y])); // Make sure the current effort is not smaller than previous effort
                        if (eff < efforts[nx][ny])
                        { // Update the minimum efforts
                            efforts[nx][ny] = eff;
                            pq.emplace(eff, nx, ny);
                        }
                    }
                }
            }
        }
        return -1;
    }
```

## Approach 2 

Binary Search


``` C++
    std::vector<std::vector<int>> dirs{{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
    int h, n;

    bool dfs(int x, int y, int threshold, std::vector<std::vector<bool>>& visited, vector<vector<int>>& heights)
    {
        if (x == h - 1 && y == n - 1)
        {
            return true;
        }

        visited[x][y] = true;

        for (auto& dir : dirs)
        {
            int nx = x + dir[0];
            int ny = y + dir[1];

            if (nx >= 0 && nx < h && ny >= 0 && ny < n && !visited[nx][ny])
            {
                int effort = std::abs(heights[nx][ny] - heights[x][y]);
                if (effort <= threshold && dfs(nx, ny, threshold, visited, heights))
                {
                    return true;
                }
            }
        }
        return false;
    }

    int minimumEffortPath(vector<vector<int>>& heights) {
        h = heights.size();
        n = heights[0].size();


        int l = 0, r = 1e6;
        int effort = 0;

        while (l <= r)
        {
            int m = l + (r - l) / 2;
            std::vector<std::vector<bool>> visited(h, std::vector<bool>(n, false));

            if (dfs(0, 0, m, visited, heights))
            {
                r = m - 1;
                effort = m;
            }
            else
            {
                l = m + 1;
            }
        }

        return effort;
    }
```
