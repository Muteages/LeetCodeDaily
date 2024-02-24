# Find All People With Secret

https://leetcode.com/problems/find-all-people-with-secret

You are given an integer n indicating there are n people numbered from 0 to n - 1. You are also given a 0-indexed 2D integer array meetings where meetings[i] = [xi, yi, timei] indicates that person xi and person yi have a meeting at timei. A person may attend multiple meetings at the same time. Finally, you are given an integer firstPerson.

Person 0 has a secret and initially shares the secret with a person firstPerson at time 0. This secret is then shared every time a meeting takes place with a person that has the secret. More formally, for every meeting, if a person xi has the secret at timei, then they will share the secret with person yi, and vice versa.

The secrets are shared instantaneously. That is, a person may receive the secret and share it with people in other meetings within the same time frame.

Return a list of all the people that have the secret after all the meetings have taken place. You may return the answer in any order.


## Approach 

``` C++
    vector<int> findAllPeople(int n, vector<vector<int>>& meetings, int firstPerson) {
        std::vector<std::vector<std::pair<int, int>>> adj(n);
        for (const auto& meeting : meetings)
        {
            int x = meeting[0], y = meeting[1], time = meeting[2];
            adj[x].emplace_back(y, time);
            adj[y].emplace_back(x, time);
        }
        std::vector<int> ans;
        std::vector<int> known(n, -1); // Store times when each person knows the secret
        std::priority_queue<std::pair<int, int>, std::vector<std::pair<int, int>>, std::greater<>> pq; // known time - person
        pq.emplace(0, 0);
        pq.emplace(0, firstPerson);
        while (!pq.empty())
        {
            auto [time, person] = pq.top();
            pq.pop();
            if (known[person] != -1)
            { // Already known the secret, skip
                continue;
            }
            ans.emplace_back(person);
            known[person] = time;
            for (const auto& [p, t] : adj[person])
            {
                if (known[p] == -1 && t >= time)
                {
                    pq.emplace(t, p);
                }
            }
        }
        
        return ans;
    }
```

