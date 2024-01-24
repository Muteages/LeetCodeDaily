# Pseudo Palindromic Paths in a Binary Tree

https://leetcode.com/problems/pseudo-palindromic-paths-in-a-binary-tree

Given a binary tree where node values are digits from 1 to 9. A path in the binary tree is said to be pseudo-palindromic if at least one permutation of the node values in the path is a palindrome.

Return the number of pseudo-palindromic paths going from the root node to leaf nodes.

## Approach 

Recursive dfs

``` C++
    int ans = 0;

    void dfs(TreeNode* node, int curr)
    {
        if (!node)
        {
            return;
        }

        curr ^= (1 << node->val);
        if (!node->left && !node->right)
        { // Leaf node. If there are more than 1 bits are '1', increment one
            ans += ((curr & (curr - 1)) == 0);
        }
        dfs(node->left, curr);
        dfs(node->right, curr);
    }

    int pseudoPalindromicPaths (TreeNode* root) {
        dfs(root, 0);
        return ans;
    }
```