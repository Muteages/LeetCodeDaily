# Island Perimeter

https://leetcode.com/problems/island-perimeter

You are given row x col grid representing a map where grid[i][j] = 1 represents land and grid[i][j] = 0 represents water.

Grid cells are connected horizontally/vertically (not diagonally). The grid is completely surrounded by water, and there is exactly one island (i.e., one or more connected land cells).

The island doesn't have "lakes", meaning the water inside isn't connected to the water around the island. One cell is a square with side length 1. The grid is rectangular, width and height don't exceed 100. Determine the perimeter of the island.

 

## Approach 1

Brute force
``` C++
    int islandPerimeter(vector<vector<int>>& grid) {
        int m = grid.size(), n = grid[0].size();
        int perimeter = 0;
        for(int row = 0; row < m; row++)
        {
            for (int col = 0; col < n; col++)
            {
                if (grid[row][col] == 1)
                { // Find a land
                    if (row - 1 < 0 || grid[row - 1][col] == 0)
                    {
                        perimeter++;
                    }
                    if (col - 1 < 0 || grid[row][col - 1] == 0)
                    {
                        perimeter++;
                    }
                    if (row + 1 == m || grid[row + 1][col] == 0)
                    {
                        perimeter++;
                    }
                    if (col + 1 == n || grid[row][col + 1] == 0)
                    {
                        perimeter++;
                    }
                }
            }
        }
        return perimeter;
```

## Approach 2

Optimised approach
``` C++
    int islandPerimeter(vector<vector<int>>& grid) {
        int m = grid.size(), n = grid[0].size();
        int perimeter = 0;
        for(int row = 0; row < m; row++)
        {
            for (int col = 0; col < n; col++)
            {
                if (grid[row][col] == 1)
                { // Find a land
                    perimeter += 4;
                    // Remove the edges which are inside
                    if (row > 0 && grid[row - 1][col] == 1)
                    {
                        perimeter -= 2;
                    }
                    if (col > 0 && grid[row][col - 1] == 1)
                    {
                        perimeter -= 2;
                    }
                }
            }
        }
        return perimeter;
    }
```

## Approach 3

DFS

``` C++
    int dfs(vector<vector<int>>& grid, int row, int col)
    {
        int m = grid.size(), n = grid[0].size();
        if (row < 0 || col < 0 || row >= m || col >= n || grid[row][col] == 0)
        {
            return 1;
        }
        if (grid[row][col] != 1)
        { // Has been visited
            return 0;
        }
        grid[row][col] = -1; // Set to visited
        return (dfs(grid, row - 1, col) + 
                dfs(grid, row + 1, col) + 
                dfs(grid, row, col - 1) +
                dfs(grid, row, col + 1));
    }

    int islandPerimeter(vector<vector<int>>& grid) {
        int perimeter = 0;
        int m = grid.size(), n = grid[0].size();
        for (int row = 0; row < m; row++)
        {
            for (int col = 0; col < n; col++)
            {
                if (grid[row][col] == 1)
                {
                    perimeter += dfs(grid, row, col); 
                    break; // Once we find a land cell, all the cells will be visited, thus break the loop here
                }
            }
            if (perimeter != 0)
            {
                break;
            }
        }
        return perimeter;
    }
```