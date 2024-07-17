# Delete Nodes and Return Forest

https://leetcode.com/problems/delete-nodes-and-return-forest

Given the root of a binary tree, each node in the tree has a distinct value.

After deleting all nodes with a value in to_delete, we are left with a forest (a disjoint union of trees).

Return the roots of the trees in the remaining forest. You may return the result in any order.

## Approach 

``` C++
    std::vector<TreeNode*> ans;
    std::bitset<1001> deletes;
    TreeNode* dfs(TreeNode* node)
    {
        if (!node)
        {
            return node;
        }
        node->left = dfs(node->left);
        node->right = dfs(node->right);
        if (!deletes[node->val])
        {
            return node;
        }
        if (node->left) ans.emplace_back(node->left);
        if (node->right) ans.emplace_back(node->right);
        delete node;
        return nullptr;
    }

    vector<TreeNode*> delNodes(TreeNode* root, vector<int>& to_delete) {
        for (int d : to_delete)
        {
            deletes[d] = 1;
        }
        root = dfs(root);
        if (root) ans.emplace_back(root); // Check if the origin root is not deleted
        return ans;
    }
```