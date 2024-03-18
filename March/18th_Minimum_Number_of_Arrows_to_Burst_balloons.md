# Minimum Number of Arrows to Burst Balloons

https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/

There are some spherical balloons taped onto a flat wall that represents the XY-plane. The balloons are represented as a 2D integer array points where points[i] = [xstart, xend] denotes a balloon whose horizontal diameter stretches between xstart and xend. You do not know the exact y-coordinates of the balloons.

Arrows can be shot up directly vertically (in the positive y-direction) from different points along the x-axis. A balloon with xstart and xend is burst by an arrow shot at x if xstart <= x <= xend. There is no limit to the number of arrows that can be shot. A shot arrow keeps traveling up infinitely, bursting any balloons in its path.

Given the array points, return the minimum number of arrows that must be shot to burst all balloons.

## Approach 1

Sort the array by their start coordinates.

``` C++
    int findMinArrowShots(vector<vector<int>>& points) {
        std::sort(points.begin(), points.end());
        int arrows = 1;
        int prevEnd = points[0][1];
        for (int i = 1; i < points.size(); i++)
        {
            if (points[i][0] > prevEnd)
            { // Indicates the current point has overlapping area with previous record, switch to a new boundrary
                arrows++;
                prevEnd = points[i][1];
            }
            else
            { // Maintain the overlapping boundrary
                prevEnd = std::min(prevEnd, points[i][1]);
            }
        }
        return arrows;
    }
```

## Approach 2

Sort the array by their end coordinates.

``` C++
    int findMinArrowShots(vector<vector<int>>& points) {
        std::sort(points.begin(), points.end(), [](const std::vector<int>& v1, const std::vector<int>& v2){
            return v1[1] < v2[1];
        });
        int arrows = 1;
        int prevEnd = points[0][1];
        for (int i = 1; i < points.size(); i++)
        {
            if (points[i][0] > prevEnd)
            {
                arrows++;
                prevEnd = points[i][1];
            }
        }
        return arrows;
    }
```