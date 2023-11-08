# Determine if a Cell Is Reachable at a Given Time

https://leetcode.com/problems/determine-if-a-cell-is-reachable-at-a-given-time

You are given four integers sx, sy, fx, fy, and a non-negative integer t.

In an infinite 2D grid, you start at the cell (sx, sy). Each second, you must move to any of its adjacent cells.

Return true if you can reach cell (fx, fy) after exactly t seconds, or false otherwise.

A cell's adjacent cells are the 8 cells around it that share at least one corner with it. You can visit the same cell several times.


## Approach 

``` C++
    bool isReachableAtTime(int sx, int sy, int fx, int fy, int t) {
        if (sx == fx && sy == fy && t == 1)
        { // Edge Case: start == target
            return false;
        }
        int gapX = std::abs(fx - sx);
        int gapY = std::abs(fy - sy);
        return t >= std::max(gapX, gapY);
    }
```