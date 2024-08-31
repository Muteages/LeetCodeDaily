# Path with Maximum Probability

https://leetcode.com/problems/path-with-maximum-probability

You are given an undirected weighted graph of n nodes (0-indexed), represented by an edge list where edges[i] = [a, b] is an undirected edge connecting the nodes a and b with a probability of success of traversing that edge succProb[i].

Given two nodes start and end, find the path with the maximum probability of success to go from start to end and return its success probability.

If there is no path from start to end, return 0. Your answer will be accepted if it differs from the correct answer by at most 1e-5.


## Approach 

``` C++
    using dNi = std::pair<double, int>;
    void initAdj(const std::vector<std::vector<int>>& edges, const std::vector<double>& succProb, std::vector<std::vector<dNi>>& adj)
    {
        int n = edges.size();
        for (int i = 0; i < n; i++)
        {
            int u = edges[i][0], v = edges[i][1];
            double prob = succProb[i];
            adj[u].emplace_back(prob, v);
            adj[v].emplace_back(prob, u);
        }
    }

    double maxProbability(int n, vector<vector<int>>& edges, vector<double>& succProb, int start_node, int end_node) {
        std::vector<std::vector<dNi>> adj(n);
        initAdj(edges, succProb, adj);

        std::priority_queue<dNi> pq;
        pq.emplace(1.0, start_node);
        std::vector<double> probs(n, 0.0);
        probs[start_node] = 1.0;

        while (!pq.empty())
        {
            auto [curProb, u] = pq.top();
            pq.pop();
            if (u == end_node) break;
            for (const auto [nextProb, v] : adj[u])
            {
                double prob = curProb * nextProb;
                if (probs[v] < prob)
                {
                    probs[v] = prob;
                    pq.emplace(prob, v);
                }
            }
        }
        return probs[end_node];
    }
```