# Binary Tree Traversal

Given the root of a binary tree, return the inorder traversal of its nodes' values.


## Approach 1

``` C++
    void inOrder(TreeNode* curr, std::vector<int>& v)
    {
        if (!curr)
        {
            return;
        }
        inOrder(curr->left, v);
        v.emplace_back(curr->val);
        inOrder(curr->right, v);
    }

    vector<int> inorderTraversal(TreeNode* root) {
        std::vector<int> ans{};
        inOrder(root, ans);
        return ans;
    }
```

## Approach 2
``` C++
    vector<int> inorderTraversal(TreeNode* root) {
        std::vector<int> ans{};
        std::stack<TreeNode*> s;

        while (root || !s.empty())
        {
            while (root)
            { // Push all left side node into the stack
                s.emplace(root);
                root = root->left;
            }
            root = s.top();
            s.pop();
            ans.emplace_back(root->val); 
            root = root->right; // Go right 
        }
        return ans;
    }
```