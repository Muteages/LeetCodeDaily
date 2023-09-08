# 01 Matrix

https://leetcode.com/problems/01-matrix/description/

Given an m x n binary matrix mat, return the distance of the nearest 0 for each cell.

The distance between two adjacent cells is 1.


# Apporach

Use BFS to solve the problem.

``` C++
    vector<vector<int>> updateMatrix(vector<vector<int>>& mat) {
        int m = mat.size();    
        int n = mat[0].size();
        
        std::queue<std::pair<int,int>> coords; // Store 0s' coordinates
        // modify the matrix in place
        for (int y = 0; y < m; y++)
        {
            for (int x = 0; x < n; x++)
            {
                if (mat[y][x] == 0)
                { // enqueue 0s into coords
                    coords.push({x, y});
                }
                else
                { // set 1 into -1 which indicates it's unvisited
                    mat[y][x] = -1;
                }
            }
        }

        std::vector<std::pair<int, int>> dir{{1, 0}, {-1, 0}, {0, 1}, {0, -1}};

        while (!coords.empty())
        {
            auto [x, y] = coords.front();
            coords.pop();

            for (auto [dx, dy] : dir)
            {
                int tempX = x + dx;
                int tempY = y + dy;
                if (tempX >= 0 && tempY >= 0 && tempX < n && tempY < m && mat[tempY][tempX] == -1)
                { // modify all unvisited cells
                    coords.push({tempX, tempY});
                    mat[tempY][tempX] = mat[y][x] + 1;
                }
            }
        }
        return mat;
    }
```