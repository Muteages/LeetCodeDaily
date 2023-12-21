# Widest Vertical Area Between Two Points Containing No Points

https://leetcode.com/problems/widest-vertical-area-between-two-points-containing-no-points

Given n points on a 2D plane where points[i] = [xi, yi], Return the widest vertical area between two points such that no points are inside the area.

A vertical area is an area of fixed-width extending infinitely along the y-axis (i.e., infinite height). The widest vertical area is the one with the maximum width.

## Approach 

``` C++
    int maxWidthOfVerticalArea(vector<vector<int>>& points) {
        std::sort(points.begin(), points.end(), 
        [](const std::vector<int>& p1, const std::vector<int>& p2)
        { // Sort by non-descending order
            return p1[0] <= p2[0];
        });
        int ans = 0;
        for (int i = 1; i < points.size(); i++)
        { // Find the maximum wide
            int temp = points[i][0] - points[i - 1][0];
            ans = std::max(ans, temp);
        }
        return ans;
    }
```

