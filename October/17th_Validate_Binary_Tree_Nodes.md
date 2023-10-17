# Validate Binary Tree Nodes

https://leetcode.com/problems/validate-binary-tree-nodes

You have n binary tree nodes numbered from 0 to n - 1 where node i has two children leftChild[i] and rightChild[i], return true if and only if all the given nodes form exactly one valid binary tree.

If node i has no left child then leftChild[i] will equal -1, similarly for the right child.


## Approach 1

DFS / BFS Iteration

``` C++
    bool validateBinaryTreeNodes(int n, vector<int>& leftChild, vector<int>& rightChild) {
        std::vector<int> parentCheck(n, -1);
        
        // Check if multi-parent exists
        for (const int& child : leftChild)
        {
            if (child != -1)
            {
                parentCheck[child] = 1;
            }
        }
        for (const int& child : rightChild)
        {
            if (child != -1)
            {
                if (parentCheck[child] == 1)
                { // Multi-parent
                    return false;
                }
                parentCheck[child] = 1;
            }
        }

        // Check if there has and only has one root
        int root = -1;
        for (int i = 0; i < n; i++)
        {
            if (parentCheck[i] == -1)
            {
                if (root != -1)
                { // Multi-root
                    return false;
                }
                root = i;
            }
        }
        if (root == -1)
        { // No root
            return false;   
        }

        // Check cycle
        std::vector<bool> visited(n, false);
        std::queue<int> bfs;
        //std::stack<int> dfs;
        bfs.emplace(root);
        while (!bfs.empty())
        {
            int curr = bfs.front();
            bfs.pop();
            
            if (visited[curr])
            { // Cycle
                return false;
            }
            visited[curr] = true;

            if (leftChild[curr] != -1)
            {
                bfs.emplace(leftChild[curr]);
            }
            if (rightChild[curr] != -1)
            {
                bfs.emplace(rightChild[curr]);
            }
        }

        // Check multi-components
        for (int i = 0; i < n; i++)
        {
            if (!visited[i])
            {
                return false;
            }
        }
        return true;
    }
```

## Approach 2

BFS Recursion

``` C++
    bool dfs(int root, std::vector<bool>& visited, std::vector<int>& leftChild, std::vector<int>& rightChild)
    {
        if (visited[root])
        { // Cycle
            return false;
        }
        visited[root] = true;

        if (leftChild[root] != -1)
        {
            if (!dfs(leftChild[root], visited, leftChild, rightChild))
            {
                return false;
            }
        }
        if (rightChild[root] != -1)
        {
            if (!dfs(rightChild[root], visited, leftChild, rightChild))
            {
                return false;
            }
        }
        return true;
    }
    bool validateBinaryTreeNodes(int n, vector<int>& leftChild, vector<int>& rightChild) {
        std::vector<int> parentCheck(n, -1);
        
        // Check if multi-parent exists
        for (const int& child : leftChild)
        {
            if (child != -1)
            {
                parentCheck[child] = 1;
            }
        }
        for (const int& child : rightChild)
        {
            if (child != -1)
            {
                if (parentCheck[child] == 1)
                { // Multi-parent
                    return false;
                }
                parentCheck[child] = 1;
            }
        }

        // Check if there has and only has one root
        int root = -1;
        for (int i = 0; i < n; i++)
        {
            if (parentCheck[i] == -1)
            {
                if (root != -1)
                { // Multi-root
                    return false;
                }
                root = i;
            }
        }
        if (root == -1)
        { // No root
            return false;   
        }

        // Check cycle
        std::vector<bool> visited(n, false);
        if (!dfs(root, visited, leftChild, rightChild))
        {
            return false;
        }

        // Check multi-component
        for (int i = 0; i < n; i++)
        {
            if (!visited[i])
            {
                return false;
            }
        }
        return true;
    }
```

