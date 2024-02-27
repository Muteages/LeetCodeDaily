# Diameter of Binary Tree

https://leetcode.com/problems/diameter-of-binary-tree

Given the root of a binary tree, return the length of the diameter of the tree.

The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

The length of a path between two nodes is represented by the number of edges between them.

## Approach 

``` C++
    int ans = 0;
    int dfs(TreeNode* node)
    {
        if (!node)
        {
            return 0;
        }
        int left = dfs(node->left);
        int right = dfs(node->right);
        ans = std::max(ans, left + right);
        return std::max(left, right) + 1;

    }
    int diameterOfBinaryTree(TreeNode* root) {
        dfs(root);
        return ans;
    }
```