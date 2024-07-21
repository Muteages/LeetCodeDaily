# Build a Matrix with Conditions

https://leetcode.com/problems/build-a-matrix-with-conditions

You are given a positive integer k. You are also given:

a 2D integer array rowConditions of size n where rowConditions[i] = [abovei, belowi], and
a 2D integer array colConditions of size m where colConditions[i] = [lefti, righti].
The two arrays contain integers from 1 to k.

You have to build a k x k matrix that contains each of the numbers from 1 to k exactly once. The remaining cells should have the value 0.

The matrix should also satisfy the following conditions:

The number abovei should appear in a row that is strictly above the row at which the number belowi appears for all i from 0 to n - 1.
The number lefti should appear in a column that is strictly left of the column at which the number righti appears for all i from 0 to m - 1.
Return any matrix that satisfies the conditions. If no answer exists, return an empty matrix.

## Approach 

Kahn's algorithm  BFS

``` C++
    std::vector<int> topoSort(std::vector<std::vector<int>>& conditions, int k)
    {
        // Kahn's algo
        std::vector<int> indegree(k + 1, 0);
        std::vector<std::vector<int>> adj(k + 1);
        for (const auto& condition : conditions)
        {
            int first = condition[0], second = condition[1];
            adj[first].emplace_back(second);
            indegree[second]++;
        }

        std::queue<int> q;
        for (int i = 1; i <= k; i++)
        {
            if (indegree[i] == 0)
            {
                q.emplace(i);
            }
        }

        std::vector<int> sorted;
        sorted.reserve(k);
        while (!q.empty())
        {
            int curr = q.front();
            q.pop();
            sorted.emplace_back(curr);
            for (int next : adj[curr])
            {
                if (--indegree[next] == 0)
                {
                    q.emplace(next);
                }
            }
        }
        if (sorted.size() != k) return {};
        return sorted;
    }

    vector<vector<int>> buildMatrix(int k, vector<vector<int>>& rowConditions, vector<vector<int>>& colConditions) {
        std::vector<int> sortedRow = topoSort(rowConditions, k);
        if (sortedRow.empty()) return {};

        std::vector<int> sortedCol = topoSort(colConditions, k);
        if (sortedCol.empty()) return {};

        std::vector<std::vector<int>> mat(k, std::vector<int>(k, 0));
        for (int row = 0; row < k; row++)
        {
            int num = sortedRow[row];
            int col = std::find(sortedCol.begin(), sortedCol.end(), num) - sortedCol.begin();
            mat[row][col] = num;
        }
        /* ** Use extra space but linear time
        std::vector<int> rows(k + 1, 0), cols(k + 1, 0);
        for (int i = 0; i < k; i++)
        {
            rows[sortedRow[i]] = i;
            cols[sortedCol[i]] = i;
        }

        for (int num = 1; num <= k; num++)
        {
            mat[rows[num]][cols[num]] = num;
        }
        */
        return mat;
    }
```

DFS

``` JavaScript
var buildMatrix = function(k, rowConditions, colConditions) {
    const topoSort = (conditions) => {
        let indeg = Array(k + 1).fill(0);
        let adj = Array.from({length : k + 1}, () => []);
        for (let condition of conditions) {
            let u = condition[0], v = condition[1];
            indeg[v]++;
            adj[u].push(v);
        }

        const st = [];
        for (let num = 1; num <= k; num++) {
            if (indeg[num] === 0) {
                st.push(num);
            }
        }

        const sorted = [];
        while (st.length > 0) {
            let curr = st.pop();
            sorted.push(curr);
            for (let next of adj[curr]) {
                if (--indeg[next] === 0) {
                    st.push(next);
                }
            }
        }

        return sorted.length === k ? sorted : [];

    };

    const sortedRow = topoSort(rowConditions), sortedCol = topoSort(colConditions);
    if (sortedRow.length === 0 || sortedCol.length === 0) {
        return [];
    }

    let mat = Array.from({length : k}, () => Array(k).fill(0));
    for (let row = 0; row < k; row++) {
        let num = sortedRow[row], col = sortedCol.indexOf(num);
        mat[row][col] = num;
    }
    return mat;
};
```