# Parallel Courses

https://leetcode.com/problems/parallel-courses-iii

You are given an integer n, which indicates that there are n courses labeled from 1 to n. You are also given a 2D integer array relations where relations[j] = [prevCoursej, nextCoursej] denotes that course prevCoursej has to be completed before course nextCoursej (prerequisite relationship). Furthermore, you are given a 0-indexed integer array time where time[i] denotes how many months it takes to complete the (i+1)th course.

You must find the minimum number of months needed to complete all the courses following these rules:

You may start taking a course at any time if the prerequisites are met.
Any number of courses can be taken at the same time.
Return the minimum number of months needed to complete all the courses.

## Approach 

``` C++
    int minimumTime(int n, vector<vector<int>>& relations, vector<int>& time) {
        // time 0-indexed, relations 1-indexed
        std::vector<std::vector<int>> adjacency(n + 1); // Node - Children
        std::vector<int> inDegrees(n + 1, 0); // 1-indexed

        // Initialise
        for (auto& relation : relations)
        {
            adjacency[relation[0]].emplace_back(relation[1]);
            inDegrees[relation[1]]++;
        }

        std::vector<int> finishTime(n + 1, 0);  // 1-indexed
        std::queue<int> q;
        for (int i = 1; i <= n; i++)
        {
            if (inDegrees[i] == 0)
            { // No previous course
                q.emplace(i);
                finishTime[i] = time[i - 1];
            }
        }

        // Kahn Algo
        while (!q.empty())
        {
            int curr = q.front();
            q.pop();

            for (auto& child : adjacency[curr])
            {
                finishTime[child] = std::max(finishTime[curr] + time[child - 1], finishTime[child]);
                if (--inDegrees[child] == 0)
                {
                    q.emplace(child);
                }
            }
        }

        int ans = *std::max_element(waitTime.begin(), waitTime.end());
        return ans;
    }
```