# Walking Robot Simulation

https://leetcode.com/problems/walking-robot-simulation

A robot on an infinite XY-plane starts at point (0, 0) facing north. The robot can receive a sequence of these three possible types of commands:

-2: Turn left 90 degrees.
-1: Turn right 90 degrees.
1 <= k <= 9: Move forward k units, one unit at a time.
Some of the grid squares are obstacles. The ith obstacle is at grid point obstacles[i] = (xi, yi). If the robot runs into an obstacle, then it will instead stay in its current location and move on to the next command.

Return the maximum Euclidean distance that the robot ever gets from the origin squared (i.e. if the distance is 5, return 25).

Note:

North means +Y direction.
East means +X direction.
South means -Y direction.
West means -X direction.
There can be obstacle in [0,0].

## Approach 1

``` C++
int robotSim(std::vector<int>& commands, std::vector<std::vector<int>>& obstacles) {
    std::unordered_map<int, std::set<int>> x2y, y2x;
    for (const auto& obs : obstacles)
    {
        x2y[obs[0]].emplace(obs[1]);
        y2x[obs[1]].emplace(obs[0]);
    }
    int dir = 0; // 0: +y | 1: +x | 2: -y | 3: -x
    int x = 0, y = 0, ans = 0;
    for (int command : commands)
    {
        if (command < 0)
        { // Change the direction
            if (command == -1)
            {
                dir = (dir + 1) % 4;
            }
            else
            {
                dir = (dir + 3) % 4;
            }
        }
        else
        { // Move following the direction
            if (dir == 0)
            { // +y
                auto it = x2y[x].upper_bound(y);
                if (it != x2y[x].end() && *it <= y + command)
                {
                    y = *it - 1;
                }
                else
                {
                    y += command;
                }
            }
            else if (dir == 1)
            { // +x
                auto it = y2x[y].upper_bound(x);
                if (it != y2x[y].end() && *it <= x + command)
                {
                    x = *it - 1;
                }
                else
                {
                    x += command;
                }
            }
            else if (dir == 2)
            { // -y
                auto it = x2y[x].lower_bound(y);
                if (it != x2y[x].begin() && *(--it) >= y - command)
                {
                    y = *it + 1;
                }
                else
                {
                    y -= command;
                }
            }
            else
            { // dir == 3 // -x
                auto it = y2x[y].lower_bound(x);
                if (it != y2x[y].begin() && *(--it) >= x - command)
                {
                    x = *it + 1;
                }
                else
                {
                    x -= command;
                }
            }
            ans = std::max(ans, x * x + y * y);
        }
    }
    return ans;
}
```

## Approach 2

``` C++
struct PairHash {
    std::size_t operator()(const std::pair<int, int>& p) const {
        return std::hash<int>{}(p.first) ^ std::hash<int>{}(p.second);
    }
};

int robotSim(std::vector<int>& commands, std::vector<std::vector<int>>& obstacles) {
    // Store obstacles in an unordered_set for O(1) access
    std::unordered_set<std::pair<int, int>, PairHash> obstacleSet;
    for (const auto& obs : obstacles) {
        obstacleSet.emplace(obs[0], obs[1]);
    }

    std::vector<std::vector<int>> dirs{{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
    int x = 0, y = 0, dir = 0, ans = 0;

    for (int command : commands)
    {
        if (command == -1)
        {
            dir = (dir + 1) % 4;  
        } 
        else if (command == -2)
        {
            dir = (dir + 3) % 4;
        } 
        else 
        {
            // Move in the current direction
            for (int i = 0; i < command; ++i) {
                int nx = x + dirs[dir][0];
                int ny = y + dirs[dir][1];
                if (obstacleSet.find({nx, ny}) != obstacleSet.end())
                {
                    break;  // Stop moving if there's an obstacle
                }
                x = nx;
                y = ny;
                ans = std::max(ans, x * x + y * y);
            }
        }
    }
    return ans;
}
```

``` JavaScript
var robotSim = function(commands, obstacles) {
    // Helper function to generate a unique string for each obstacle pair
    function encodePair(x, y) {
        return `${x},${y}`;
    }

    // Store obstacles in a Set for O(1) access
    const obstacleSet = new Set();
    for (const [x, y] of obstacles) {
        obstacleSet.add(encodePair(x, y));
    }

    // Direction vectors for up, right, down, and left
    const dirs = [[0, 1], [1, 0], [0, -1], [-1, 0]];
    let x = 0, y = 0, dir = 0, ans = 0;

    for (const command of commands) {
        if (command === -1) {
            dir = (dir + 1) % 4;
        } else if (command === -2) {
            dir = (dir + 3) % 4;
        } else {
            // Move in the current direction
            for (let i = 0; i < command; ++i) {
                const nx = x + dirs[dir][0];
                const ny = y + dirs[dir][1];
                if (obstacleSet.has(encodePair(nx, ny))) {
                    break;  // Stop moving if there's an obstacle
                }
                x = nx;
                y = ny;
                ans = Math.max(ans, x * x + y * y);
            }
        }
    }
    return ans;
};
```