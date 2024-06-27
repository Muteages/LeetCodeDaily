# Find Center of Star Graph

https://leetcode.com/problems/find-center-of-star-graph

There is an undirected star graph consisting of n nodes labeled from 1 to n. A star graph is a graph where there is one center node and exactly n - 1 edges that connect the center node with every other node.

You are given a 2D integer array edges where each edges[i] = [ui, vi] indicates that there is an edge between the nodes ui and vi. Return the center of the given star graph.

## Approach 1

``` JavaScript
var findCenter = function(edges) {
    let deg = {};
    for (let edge of edges) {
        for (let node of edge) {
            if (deg[node]) {
                return node;
            }
            deg[node] = 1;
        }
    }
    return -1;
};
```

## Approach 2

``` JavaScript
var findCenter = function(edges) {
    const [[a, b], [c, d]] = edges;
    return b === c || b === d ? b : a;
};
```