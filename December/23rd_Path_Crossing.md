# Path Crossing

https://leetcode.com/problems/path-crossing

Given a string path, where path[i] = 'N', 'S', 'E' or 'W', each representing moving one unit north, south, east, or west, respectively. You start at the origin (0, 0) on a 2D plane and walk on the path specified by path.

Return true if the path crosses itself at any point, that is, if at any time you are on a location you have previously visited. Return false otherwise.

## Approach 

``` C++
    bool isPathCrossing(string path) {
        std::set<std::pair<int, int>> visited;
        int x = 0;
        int y = 0;
        visited.emplace(x, y);
        for (const auto& p : path)
        {
            if (p == 'N')
            {
                x += 1;
                if (visited.count({x, y}))
                {
                    return true;
                }
                visited.emplace(x, y);
            }
            else if (p == 'S')
            {
                x -= 1;
                if (visited.count({x, y}))
                {
                    return true;
                }
                visited.emplace(x, y);
            }
            else if (p == 'E')
            {
                y += 1;
                if (visited.count({x, y}))
                {
                    return true;
                }
                visited.emplace(x, y);
            }
            else
            {
                y -= 1;
                if (visited.count({x, y}))
                {
                    return true;
                }
                visited.emplace(x, y);
            }
        }
        return false;
    }
```