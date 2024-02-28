# Find Bottom Left Tree Value

Given the root of a binary tree, return the leftmost value in the last row of the tree.

## Approach 

``` C++
    int findBottomLeftValue(TreeNode* root) {
        std::queue<TreeNode*> q;
        q.emplace(root);
        int leftmost{};
        while (!q.empty())
        {
            TreeNode* curr = q.front();
            leftmost = curr->val;
            q.pop();
            // post order
            if (curr->right)
            {
                q.emplace(curr->right);
            }
            if (curr->left)
            {
                q.emplace(curr->left);
            }
        }
        return leftmost;
    }
```