# Add One Row to Tree

https://leetcode.com/problems/add-one-row-to-tree

Given the root of a binary tree and two integers val and depth, add a row of nodes with value val at the given depth depth.

Note that the root node is at depth 1.

The adding rule is:

Given the integer depth, for each not null tree node cur at the depth depth - 1, create two tree nodes with value val as cur's left subtree root and right subtree root.
cur's original left subtree should be the left subtree of the new left subtree root.
cur's original right subtree should be the right subtree of the new right subtree root.
If depth == 1 that means there is no depth depth - 1 at all, then create a tree node with value val as the new root of the whole original tree, and the original tree is the new root's left subtree.

## Approach  1

BFS

``` C++
    TreeNode* addOneRow(TreeNode* root, int val, int depth) {
        if (depth == 1)
        { // Add a new root
            TreeNode* newRoot = new TreeNode(val);
            newRoot->left = root;
            return newRoot;
        }

        int curDepth = 0;
        std::queue<TreeNode*> q;
        q.emplace(root);

        // Iterate until find the depth - 1 level
        while (curDepth < depth - 2)
        { 
            curDepth++;
            TreeNode* curr = nullptr;
            int layerCount = q.size();
            while (layerCount--)
            {
                curr = q.front();
                q.pop();
                if (curr->left) q.emplace(curr->left);
                if (curr->right) q.emplace(curr->right);
            }
        }
        // Insert a row
        while (!q.empty())
        {
            TreeNode* father = q.front();
            q.pop();
            TreeNode* newLeft = new TreeNode(val, father->left, nullptr);
            father->left = newLeft;
            TreeNode* newRight = new TreeNode(val, nullptr, father->right);
            father->right = newRight;
        }
        return root;
    }
```

## Approach 2

DFS

``` C++
    void dfs(TreeNode* node, int val, int depth, int curDepth)
    {
        if (!node)
        {
            return;
        }
        if (curDepth < depth - 1)
        {
            dfs(node->left, val, depth, curDepth + 1);
            dfs(node->right, val, depth, curDepth + 1);
        }
        else
        {
            TreeNode* newLeft = new TreeNode(val, node->left, nullptr);
            node->left = newLeft;
            TreeNode* newRight = new TreeNode(val, nullptr, node->right);
            node->right = newRight;
        }
    }

    TreeNode* addOneRow(TreeNode* root, int val, int depth) {
        if (depth == 1)
        { // Add a new root
            TreeNode* newRoot = new TreeNode(val);
            newRoot->left = root;
            return newRoot;
        }
        dfs(root, val, depth, 1);
        return root;
    }
```