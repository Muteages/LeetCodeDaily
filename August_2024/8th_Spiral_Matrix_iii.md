# Spiral Matrix III

https://leetcode.com/problems/spiral-matrix-iii

You start at the cell (rStart, cStart) of an rows x cols grid facing east. The northwest corner is at the first row and column in the grid, and the southeast corner is at the last row and column.

You will walk in a clockwise spiral shape to visit every position in this grid. Whenever you move outside the grid's boundary, we continue our walk outside the grid (but may return to the grid boundary later.). Eventually, we reach all rows * cols spaces of the grid.

Return an array of coordinates representing the positions of the grid in the order you visited them.

## Approach 1

``` C++
    inline bool isInside(int r, int c, int row, int col)
    {
        return r >= 0 && r < row && c >= 0 && c < col;
    }

    vector<vector<int>> spiralMatrixIII(int rows, int cols, int rStart, int cStart) {
        int visited = 1, n = rows * cols;
        std::vector<std::vector<int>> ans(n);
        ans[0] = {rStart, cStart};
        int r = rStart, c = cStart, layer = 1;
        while (visited < n)
        {
            // Right
            while (c < cStart + layer)
            {
                c++;
                if (isInside(r, c, rows, cols))
                {
                    ans[visited++] = {r, c};
                }
            }

            // Down
            while (r < rStart + layer)
            {
                r++;
                if (isInside(r, c, rows, cols))
                {
                    ans[visited++] = {r, c};
                }
            }

            // Left
            while (c > cStart - layer)
            {
                c--;
                if (isInside(r, c, rows, cols))
                {
                    ans[visited++] = {r, c};
                }
            }

            // Up
            while (r > rStart - layer)
            {
                r--;
                if (isInside(r, c, rows, cols))
                {
                    ans[visited++] = {r, c};
                }
            }

            layer++;
        }
        return ans;
    }
```

## Approach 2

``` C++
    inline bool isInside(int r, int c, int row, int col)
    {
        return r >= 0 && r < row && c >= 0 && c < col;
    }

    vector<vector<int>> spiralMatrixIII(int rows, int cols, int rStart, int cStart) {
        int visited = 1, n = rows * cols;
        std::vector<std::vector<int>> ans(n);
        ans[0] = {rStart, cStart};
        int r = rStart, c = cStart, layer = 1;
        std::vector<std::vector<int>> dir{{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
        int dirIdx = 0;
        while (visited < n)
        {
            for (int i = 0; i < 2; i++)
            {
                for (int j = 0; j < layer; j++)
                {
                    r += dir[dirIdx][0];
                    c += dir[dirIdx][1];
                    if (isInside(r, c, rows, cols))
                    {
                        ans[visited++] = {r, c};
                    }
                }
                dirIdx = (dirIdx + 1) % 4; // Change direction
            }
            layer++; // Increase layer for every 2 directions
        }
        return ans;
    }
```