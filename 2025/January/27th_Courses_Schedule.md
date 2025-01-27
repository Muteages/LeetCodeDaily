# Courses Schedule

https://leetcode.com/problems/course-schedule-iv

There are a total of numCourses courses you have to take, labeled from 0 to numCourses - 1. You are given an array prerequisites where prerequisites[i] = [ai, bi] indicates that you must take course ai first if you want to take course bi.

For example, the pair [0, 1] indicates that you have to take course 0 before you can take course 1.
Prerequisites can also be indirect. If course a is a prerequisite of course b, and course b is a prerequisite of course c, then course a is a prerequisite of course c.

You are also given an array queries where queries[j] = [uj, vj]. For the jth query, you should answer whether course uj is a prerequisite of course vj or not.

Return a boolean array answer, where answer[j] is the answer to the jth query.

## Approach 1

BFS
``` C++
    vector<bool> checkIfPrerequisite(int numCourses, vector<vector<int>>& prerequisites, vector<vector<int>>& queries) {

        const int nq = queries.size();
        std::vector<bool> ans(nq, false);
        if (numCourses == 0 || prerequisites.empty()) return ans; // Constraints

        std::vector<std::vector<bool>> reachable(numCourses, std::vector<bool>(numCourses, false));
        std::vector<std::vector<int>> adj(numCourses);
        for (const auto& p : prerequisites)
        {
            int pre = p[0], post = p[1];
            reachable[pre][post] = 1;
            adj[pre].emplace_back(post);
        }

        for (int i = 0; i < numCourses; i++)
        {
            std::vector<bool> visited(numCourses, false);
            visited[i] = true;
            reachable[i][i] = true;
            std::queue<int> q{};
            q.emplace(i);
            while (!q.empty())
            {
                int curr = q.front();
                q.pop();
                for (int next : adj[curr])
                {
                    if (visited[next]) continue;

                    reachable[i][next] = true;
                    visited[next] = true;
                    q.emplace(next);
                }
            }
        }

        for (int i = 0; i < nq; i++)
        {
            int u = queries[i][0], v = queries[i][1];
            ans[i] = reachable[u][v];
        }
        return ans;
    }
```

``` Python
    def checkIfPrerequisite(self, numCourses: int, prerequisites: List[List[int]], queries: List[List[int]]) -> List[bool]:
        adj = [[] for _ in range(numCourses)]
        reachable = [[False] * numCourses for _ in range(numCourses)]

        for pre, post in prerequisites:
            adj[pre].append(post)
            reachable[pre][post] = True

        for i in range(numCourses):
            visited = [False] * numCourses
            visited[i] = True
            q = deque()
            q.append(i)
            while q:
                u = q.popleft()
                for v in adj[u]:
                    if visited[v]:
                        continue
                    
                    reachable[i][v] = True
                    visited[v] = True
                    q.append(v)
        
        nq = len(queries)
        ans = [[] * nq for _ in range(nq)]
        for i in range(nq):
            ans[i] = reachable[queries[i][0]][queries[i][1]]

        return ans
```

## Approach 2

DFS

``` C++
    void dfs(const std::vector<std::vector<int>>& adj, std::vector<std::vector<bool>>& reachable, std::vector<bool>& visited, int st, int curr)
    {
        visited[curr] = true;
        reachable[st][curr] = true;
        for (int next : adj[curr])
        {
            if (visited[next]) continue;

            visited[next] = true;
            reachable[st][next] = true;
            dfs(adj, reachable, visited, st, next);
        }

    }

    vector<bool> checkIfPrerequisite(int numCourses, vector<vector<int>>& prerequisites, vector<vector<int>>& queries) {

        const int nq = queries.size();
        std::vector<bool> ans(nq, false);
        if (numCourses == 0 || prerequisites.empty()) return ans;

        std::vector<std::vector<bool>> reachable(numCourses, std::vector<bool>(numCourses, false));
        std::vector<std::vector<int>> adj(numCourses);
        for (const auto& p : prerequisites)
        {
            int pre = p[0], post = p[1];
            reachable[pre][post] = 1;
            adj[pre].emplace_back(post);
        }

        for (int i = 0; i < numCourses; i++)
        {
            std::vector<bool> visited(numCourses, false);
            if (!visited[i]) dfs(adj, reachable, visited, i, i);
        }

        for (int i = 0; i < nq; i++)
        {
            int u = queries[i][0], v = queries[i][1];
            ans[i] = reachable[u][v];
        }
        return ans;
    }
```

``` Python
class Solution:
    def dfs(self, adj: List[List[int]], reachable: List[List[int]], visited: List[bool], st: int, curr: int):
        for next_node in adj[curr]:
            if not visited[next_node]:
                visited[next_node] = True
                reachable[st][next_node] = True
                self.dfs(adj, reachable, visited, st, next_node)


    def checkIfPrerequisite(self, numCourses: int, prerequisites: List[List[int]], queries: List[List[int]]) -> List[bool]:
        adj = [[] for _ in range(numCourses)]
        reachable = [[False] * numCourses for _ in range(numCourses)]

        for pre, post in prerequisites:
            adj[pre].append(post)
            reachable[pre][post] = True

        for i in range(numCourses):
            visited = [False] * numCourses
            self.dfs(adj, reachable, visited, i, i)
        
        nq = len(queries)
        ans = [False] * nq
        for i in range(nq):
            ans[i] = reachable[queries[i][0]][queries[i][1]]
        return ans
```