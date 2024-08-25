# Postorder Traversal

https://leetcode.com/problems/binary-tree-postorder-traversal

Given the root of a binary tree, return the postorder traversal of its nodes' values.

## Approach 

``` C++
    std::vector<int> ans{};
    vector<int> postorderTraversal(TreeNode* root) {
        if (!root) return ans;
        postorderTraversal(root->left);
        postorderTraversal(root->right);
        ans.emplace_back(root->val);
        return ans;
    }
```