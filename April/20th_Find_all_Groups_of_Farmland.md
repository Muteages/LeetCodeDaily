# Find All Groups of Farmland


https://leetcode.com/problems/find-all-groups-of-farmland/

You are given a 0-indexed m x n binary matrix land where a 0 represents a hectare of forested land and a 1 represents a hectare of farmland.

To keep the land organized, there are designated rectangular areas of hectares that consist entirely of farmland. These rectangular areas are called groups. No two groups are adjacent, meaning farmland in one group is not four-directionally adjacent to another farmland in a different group.

land can be represented by a coordinate system where the top left corner of land is (0, 0) and the bottom right corner of land is (m-1, n-1). Find the coordinates of the top left and bottom right corner of each group of farmland. A group of farmland with a top left corner at (r1, c1) and a bottom right corner at (r2, c2) is represented by the 4-length array [r1, c1, r2, c2].

Return a 2D array containing the 4-length arrays described above for each group of farmland in land. If there are no groups of farmland, return an empty array. You may return the answer in any order.


## Approach 

``` C++
    std::vector<std::vector<int>> farmlands{};
    int m{}, n{};

    bool isFarmland(vector<vector<int>>& land, int row, int col)
    {
        return (row >= 0 && row < m && col >= 0 && col < n && land[row][col] == 1);
    }

    bool isRightBottomLand(vector<vector<int>>& land, int row, int col)
    {
        return ((row == m - 1 || land[row + 1][col] == 0) && 
                (col == n - 1 || land[row][col + 1] == 0));
    }

    void dfs(vector<vector<int>>& land, int row, int col)
    {
        if (!isFarmland(land, row, col))
        {
            return;
        }
        
        land[row][col] = 2; // Set as visited
        if (isRightBottomLand(land, row, col))
        { // Update the corresponding right bootom corner coordinate
            farmlands.back()[2] = row;
            farmlands.back()[3] = col;
            return;
        }
        dfs(land, row - 1, col);
        dfs(land, row + 1, col);
        dfs(land, row, col - 1);
        dfs(land, row, col + 1);
    }

    vector<vector<int>> findFarmland(vector<vector<int>>& land) {
        m = land.size();
        n = land[0].size();
        for (int row = 0; row < m; row++)
        {
            for (int col = 0; col < n; col++)
            {
                if (land[row][col] == 1)
                {
                    std::vector<int> farmland = {row, col, 0, 0};
                    farmlands.emplace_back(std::move(farmland)); // Insert the left corner coordinate first;
                    dfs(land, row, col);
                }
            }
        }
        return std::move(farmlands);
    }
```