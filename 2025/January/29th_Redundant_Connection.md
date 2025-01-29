# Redundant Connection

https://leetcode.com/problems/redundant-connection

In this problem, a tree is an undirected graph that is connected and has no cycles.

You are given a graph that started as a tree with n nodes labeled from 1 to n, with one additional edge added. The added edge has two different vertices chosen from 1 to n, and was not an edge that already existed. The graph is represented as an array edges of length n where edges[i] = [ai, bi] indicates that there is an edge between nodes ai and bi in the graph.

Return an edge that can be removed so that the resulting graph is a tree of n nodes. If there are multiple answers, return the answer that occurs last in the input.

## Approach 

Union Find

``` C++
    class UnionFind
    {
    public:
        UnionFind(int n)
        {
            rank.resize(n, 1);
            parent.resize(n);
            std::iota(parent.begin(), parent.end(), 0);
        }

        int find(int node)
        {
            if (parent[node] != node)
            {
                return find(parent[node]);
            }
            return parent[node];
        }

        bool unionSet(int n1, int n2)
        {
            int p1 = find(n1), p2 = find(n2);

            if (p1 == p2) return false;

            if (rank[p1] > rank[p2])
            {
                parent[p2] = p1;
            }
            else if (rank[p1] < rank[p2])
            {
                parent[p1] = p2;
            }
            else
            {
                parent[p2] = p1;
                rank[p1]++;
            }
            return true;
        }

    private:
        std::vector<int> parent;
        std::vector<int> rank;
    };

    vector<int> findRedundantConnection(vector<vector<int>>& edges) {
        const int n = edges.size();
        UnionFind uf(n + 1);

        for (const auto& edge : edges)
        {
            int u = edge[0], v = edge[1];
            if (!uf.unionSet(u, v))
            {
                return edge;
            }
        }
        return {};
    }
```

``` Python
class UnionFind:
    def __init__(self, n: int):
        self.parent = list(range(n))
        self.rank = [1] * n

    def find(self, num: int) -> int:
        if self.parent[num] != num:
            self.parent[num] = self.find(self.parent[num])
        return self.parent[num]
    
    def union_set(self, n1: int, n2: int) -> bool:
        p1, p2 = self.find(n1), self.find(n2)
        if p1 == p2:
            return False
        
        if self.rank[p1] > self.rank[p2]:
            self.parent[p2] = p1
        elif self.rank[p1] < self.rank[p2]:
            self.parent[p1] = p2
        else:
            self.parent[p2] = p1
            self.rank[p1] += 1
        return True 


class Solution:
    def findRedundantConnection(self, edges: List[List[int]]) -> List[int]:
        uf = UnionFind(len(edges) + 1)

        for edge in edges:
            if not uf.union_set(edge[0], edge[1]):
                return edge
        
        return []
```

``` JavaScript
class UnionFind {
    constructor(n) {
        this.parent = Array.from({length: n}, (_, i) => i);
        this.rank = new Array(n).fill(1);
    }

    find(num) {
        if (this.parent[num] !== num) {
            this.parent[num] = this.find(this.parent[num]);
        }
        return this.parent[num];
    }

    unionSet(n1, n2) {
        const p1 = this.find(n1), p2 = this.find(n2);

        if (p1 === p2) return false;

        if (this.rank[p1] > this.rank[p2]) {
            this.parent[p2] = p1;
        } else if (this.rank[p1] < this.rank[p2]) {
            this.parent[p1] = p2;
        } else {
            this.parent[p2] = p1;
            this.rank[p1]++;
        }
        return true;
    }
};

var findRedundantConnection = function(edges) {
    uf = new UnionFind(edges.length + 1);

    for (const edge of edges) {
        if (!uf.unionSet(edge[0], edge[1])) {
            return edge;
        }
    }    
    return [];
};
```