# Even Odd Tree

https://leetcode.com/problems/even-odd-tree

A binary tree is named Even-Odd if it meets the following conditions:

The root of the binary tree is at level index 0, its children are at level index 1, their children are at level index 2, etc.
For every even-indexed level, all nodes at the level have odd integer values in strictly increasing order (from left to right).
For every odd-indexed level, all nodes at the level have even integer values in strictly decreasing order (from left to right).
Given the root of a binary tree, return true if the binary tree is Even-Odd, otherwise return false.

## Approach 

``` C++
    bool isEvenOddTree(TreeNode* root) {
        std::queue<TreeNode*> q;
        q.emplace(root);
        bool isEvenLayer = false;
        while (!q.empty())
        {
            isEvenLayer = !isEvenLayer;
            int n = q.size();
            int prev =  isEvenLayer ? 0 : 1e6 + 1;
            for (int i = 0; i < n; i++)
            {
                TreeNode* curr = q.front();
                q.pop();
                if (!curr)
                {
                    continue;
                }
                if ((isEvenLayer && (curr->val <= prev || curr->val % 2 == 0)) ||
                    (!isEvenLayer && (curr->val >= prev || curr->val % 2 != 0)))
                {
                    return false;  
                }
                prev = curr->val;
                q.emplace(curr->left);
                q.emplace(curr->right);
            }
        }
        return true;
    }
```