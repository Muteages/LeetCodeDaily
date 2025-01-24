# Find Eventual Safe States

https://leetcode.com/problems/find-eventual-safe-states

There is a directed graph of n nodes with each node labeled from 0 to n - 1. The graph is represented by a 0-indexed 2D integer array graph where graph[i] is an integer array of nodes adjacent to node i, meaning there is an edge from node i to each node in graph[i].

A node is a terminal node if there are no outgoing edges. A node is a safe node if every possible path starting from that node leads to a terminal node (or another safe node).

Return an array containing all the safe nodes of the graph. The answer should be sorted in ascending order.

## Approach 

``` C++
    bool isSafeNode(std::vector<std::vector<int>>& graph, std::vector<int>& states, int curr)
    {
        if (states[curr] != -1)
        {
            return states[curr];
        }

        states[curr] = 0;
        for (const int next : graph[curr])
        {
            if (states[next] == 0 || !isSafeNode(graph, states, next))
            {
                return false;
            }
        }
        return states[curr] = 1;
    }

    vector<int> eventualSafeNodes(vector<vector<int>>& graph) {
        const int n = graph.size();
        std::vector<int> states(n, -1); // -1: unvisited, 0: visiting(unsafe for now), 1: safe

        std::vector<int> ans{};
        ans.reserve(n);
        for (int i = 0; i < n; i++)
        {
            if (isSafeNode(graph, states, i))
            {
                ans.emplace_back(i);
            }
        }
        return ans;
    }
```

``` Python
    def eventualSafeNodes(self, graph: List[List[int]]) -> List[int]:
        n = len(graph)
        states = [-1] * n # -1: unvisited   0: visiting(unsafe for now) 1: safe

        def is_safe(curr) -> bool:
            if states[curr] != -1:
                return states[curr]
            
            states[curr] = 0
            for next in graph[curr]:
                if states[next] == 0 or not is_safe(next):
                    return False
            
            states[curr] = 1
            return True
        
        return [node for node in range(n) if is_safe(node)]
```

``` JavaScript
var eventualSafeNodes = function(graph) {
    const n = graph.length;
    const states = new Array(n).fill(-1);
    const isSafe = (curr) => {
        if (states[curr] != -1) return states[curr];
        states[curr] = 0;

        for (let next of graph[curr]) {
            if (states[next] == 0 || !isSafe(next)) {
                return false;
            }
        }
        return states[curr] = 1;
    };

    return [...Array(n).keys()].filter(isSafe);
};
```

