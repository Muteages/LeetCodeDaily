# Image Smoother

https://leetcode.com/problems/image-smoother

An image smoother is a filter of the size 3 x 3 that can be applied to each cell of an image by rounding down the average of the cell and the eight surrounding cells. Given an m x n integer matrix img representing the grayscale of an image, return the image after applying the smoother on each cell of it.

## Approach 

``` C++
    vector<vector<int>> imageSmoother(vector<vector<int>>& img) {
        int m = img.size();
        int n = img[0].size();
        std::vector<std::vector<int>> ans(m, std::vector<int>(n, 0));
        std::vector<std::vector<int>> dirs{{1, 0}, {1, 1}, {0, 1}, {-1, 1}, {-1, 0}, {-1, -1}, {0, -1}, {1, -1}};

        for (int row = 0; row < m; row++)
        {
            for (int col = 0; col < n; col++)
            {
                // Count itself in first
                int sum = img[row][col];
                int cnt = 1;
                for (auto& dir : dirs)
                {
                    int neighbourRow = row + dir[0];
                    int neighbourCol = col + dir[1];
                    if ((neighbourRow >= 0 && neighbourRow < m) && (neighbourCol >= 0 && neighbourCol < n))
                    { // Valid neighbour
                        sum += img[neighbourRow][neighbourCol];
                        cnt++;
                    }
                }
                ans[row][col] = std::floor(sum / cnt);
            }
        }
        return ans;
    }
```