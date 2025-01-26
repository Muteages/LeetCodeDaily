# Maximum Employees to be Invited to A Meeting

https://leetcode.com/problems/maximum-employees-to-be-invited-to-a-meeting

A company is organizing a meeting and has a list of n employees, waiting to be invited. They have arranged for a large circular table, capable of seating any number of employees.

The employees are numbered from 0 to n - 1. Each employee has a favorite person and they will attend the meeting only if they can sit next to their favorite person at the table. The favorite person of an employee is not themself.

Given a 0-indexed integer array favorite, where favorite[i] denotes the favorite person of the ith employee, return the maximum number of employees that can be invited to the meeting.

## Approach 

Khan's Algo and Topological Sort

``` C++
    int maximumInvitations(vector<int>& favorite) {
        const int n = favorite.size();
        // Kahn's Algo
        // Count in degree of each node
        std::vector<int> deg(n);
        for (int fav : favorite)
        {
            deg[fav]++;
        }

        // Find leave nodes, i.e deg == 0
        std::queue<int> q{};
        for (int i = 0; i < n; i++)
        {
            if (deg[i] == 0) q.emplace(i);
        }

        // Calculate each chain's max length
        std::vector<int> chainLens(n, 1); // Including itself first
        for (int len = 1; !q.empty(); len++)
        {
            int sz = q.size();
            for (int i = 0; i < sz; i++)
            {
                int curr = q.front();
                q.pop();
                int next = favorite[curr];
                chainLens[next] = std::max(chainLens[next], len + 1);
                if (--deg[next] == 0) q.emplace(next);
            }
        }

        // Compare two cases: 1: a full cycle. 2: two chains with some 2-cycle
        int maxCycle = 0, combined = 0;
        for (int i = 0; i < n; i++)
        {
            if (deg[i] == 0) continue;

            int cycle = 0;
            for (int j = i; deg[j] != 0; j = favorite[j])
            {
                cycle++;
                deg[j] = 0; // Mark as visited
            }

            if (cycle == 2)
            {
                combined += chainLens[i] + chainLens[favorite[i]];
            }
            else
            {
                maxCycle = std::max(maxCycle, cycle);
            }
        }
        return std::max(maxCycle, combined);
    }
```

``` Python
    def maximumInvitations(self, favorite: List[int]) -> int:
        n = len(favorite)
        deg = [0] * n
        for fav in favorite:
            deg[fav] += 1
        
        q = deque()
        for i in range(n):
            if deg[i] == 0:
                q.append(i)
        
        chain_lens = [1] * n
        while q:
            sz = len(q)
            for i in range(sz):
                curr = q.popleft()
                next_node = favorite[curr]
                chain_lens[next_node] = max(chain_lens[next_node], chain_lens[curr] + 1)
                deg[next_node] -= 1
                if deg[next_node] == 0:
                    q.append(next_node)
        

        max_cycle_len, combined = 0, 0
        for i in range(n):
            if deg[i] == 0:
                continue
            
            cycle_len = 0
            j = i
            while deg[j] != 0:
                cycle_len += 1
                deg[j] = 0
                j = favorite[j]
            
            if cycle_len == 2:
                combined += chain_lens[i] + chain_lens[favorite[i]]
            else:
                max_cycle_len = max(max_cycle_len, cycle_len)
        
        return max(max_cycle_len, combined)
```

``` JavaScript
var maximumInvitations = function(favorite) {
    const n = favorite.length;
    const deg = new Array(n).fill(0);
    for (const fav of favorite) {
        deg[fav]++;
    }

    const q = [];
    for (let i = 0; i < n; i++) {
        if (deg[i] === 0) {
            q.push(i);
        }
    }


    const chainLens = new Array(n).fill(1);
    head = 0;
    while (head <= q.length) {
        // shift 
        const curr = q[head++];
        const next = favorite[curr];
        chainLens[next] = Math.max(chainLens[next], chainLens[curr] + 1);
        if (--deg[next] === 0) {
            q.push(next);
        }
    }

    let maxCycle = 0, combined = 0;
    for (let i = 0; i < n; i++) {
        if (deg[i] === 0) continue;

        let curCycle = 0;
        for (let j = i; deg[j] !== 0; j = favorite[j]) {
            deg[j] = 0;
            curCycle++;
        }

        if (curCycle === 2) {
            combined += chainLens[i] + chainLens[favorite[i]];
        } else {
            maxCycle = Math.max(maxCycle, curCycle);
        }
    }
    return Math.max(maxCycle, combined);
};
```