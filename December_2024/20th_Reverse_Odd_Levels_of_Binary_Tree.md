# Reverse Odd Levels of Binary Tree

Given the root of a perfect binary tree, reverse the node values at each odd level of the tree.

A binary tree is perfect if all parent nodes have two children and all leaves are on the same level.

The level of a node is the number of edges along the path between it and the root node.


## Approach 1

BFS
``` C++
    TreeNode* reverseOddLevels(TreeNode* root) {
        bool isOdd = false; // Start from level 0
        std::queue<TreeNode*> bfs{};
        bfs.emplace(root);
        while (!bfs.empty())
        {
            int n = bfs.size();
            std::vector<TreeNode*> curLayer(n);
            for (int i = 0; i < n; i++)
            {
                TreeNode* curr = bfs.front();
                bfs.pop();
                if (curr->left)
                { // Since the trre is perfect, only check one child status
                    bfs.emplace(curr->left);
                    bfs.emplace(curr->right);
                }
                if (isOdd)
                {
                    curLayer[i] = curr;
                    if (i >= n / 2)
                    {
                        std::swap(curLayer[i]->val, curLayer[n - 1 -i]->val);
                    }
                }
            }
            isOdd = !isOdd;
        }
        return root;
    }
```

## Approach 2

DFS
``` JavaScript
var reverseOddLevels = function(root) {
    const dfs = (node1, node2, isOdd) => {
        if (!node1) return;

        if (isOdd) {
            [node1.val, node2.val] = [node2.val, node1.val];
        }
        dfs(node1.left, node2.right, !isOdd);
        dfs(node1.right, node2.left, !isOdd);
    };

    dfs(root.left, root.right, true);
    return root;
};
```