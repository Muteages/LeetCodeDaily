# Open the Lock

https://leetcode.com/problems/open-the-lock

You have a lock in front of you with 4 circular wheels. Each wheel has 10 slots: '0', '1', '2', '3', '4', '5', '6', '7', '8', '9'. The wheels can rotate freely and wrap around: for example we can turn '9' to be '0', or '0' to be '9'. Each move consists of turning one wheel one slot.

The lock initially starts at '0000', a string representing the state of the 4 wheels.

You are given a list of deadends dead ends, meaning if the lock displays any of these codes, the wheels of the lock will stop turning and you will be unable to open it.

Given a target representing the value of the wheels that will unlock the lock, return the minimum total number of turns required to open the lock, or -1 if it is impossible.

## Approach 1

``` C++
    int openLock(vector<string>& deadends, string target) {
        std::vector<bool> visited(10000, false);
        for (const auto& deadend : deadends)
        {
            visited[std::stoi(deadend)] = true;
        }
        if (visited[0])
        {
            return -1;
        }
        std::queue<std::pair<std::string, int>> bfs; // current string - counts so far
        bfs.emplace("0000", 0);
        while (!bfs.empty())
        {
            auto [curr, cnt] = bfs.front();
            bfs.pop();
            if (curr == target)
            {
                return cnt;
            }
            for (int digit = 0; digit < 4; digit++)
            { // Modify all four digits
                for (int offset : {1, -1})
                { // +1 / -1 for each digit
                    std::string next = curr;
                    char& ch = next[digit];
                    ch = (ch - '0' + offset + 10) % 10 + '0';
                    int num = std::stoi(next);
                    if (!visited[num])
                    {
                        bfs.emplace(next, cnt + 1);
                        visited[num] = true;
                    }
                }
            }
        }
        return -1;
    }
```

## Approach 2

Optimal solution using bitset

``` C++
    int openLock(vector<string>& deadends, string target) {
        std::bitset<10000> visited = 0;
        for (const auto& deadend : deadends)
        {
            visited[std::stoi(deadend)] = 1;
        }
        if (visited[0])
        {
            return -1;
        }

        std::queue<std::pair<int, int>> bfs; // current number - counts so far
        bfs.emplace(0, 0);
        const int targetNumber = std::stoi(target);
        std::vector<int> digs = {1, 10, 100, 1000};
        while (!bfs.empty())
        {
            auto [curr, cnt] = bfs.front();
            bfs.pop();
            if (targetNumber == curr)
            {
                return cnt;
            }
            int curDigit{}, num = curr;
            for (int digit = 0; digit < 4; digit++)
            {
                curDigit = num % 10;
                num /= 10;
                for (int offset : {1, -1})
                {
                    int nextDigit = (curDigit + offset + 10) % 10;
                    int next = curr + (nextDigit - curDigit) * digs[digit];
                    if (!visited[next])
                    {
                        bfs.emplace(next, cnt + 1);
                        visited[next] = 1;
                    }
                }
            }
        }
        return -1;
    }
```