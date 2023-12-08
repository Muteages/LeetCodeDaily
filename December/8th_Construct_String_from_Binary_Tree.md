# Construct String from Binary Tree

https://leetcode.com/problems/construct-string-from-binary-tree


Given the root of a binary tree, construct a string consisting of parenthesis and integers from a binary tree with the preorder traversal way, and return it.

Omit all the empty parenthesis pairs that do not affect the one-to-one mapping relationship between the string and the original binary tree.

## Approach 

``` C++
class Solution {
private:
    std::string ans;
    void dfs(TreeNode* curr, std::string& s)
    {
        if (curr == nullptr)
        {
            return;
        }
        // pre-order
        s += std::to_string(curr->val);
        if (curr->left || curr->right)
        {
            s += "(";
            dfs(curr->left, s);
            s += ")";
        }
        if (curr->right)
        {
            s += "(";
            dfs(curr->right, s);
            s += ")";
        }
    }
public:
    string tree2str(TreeNode* root) {
        std::string ans{};
        dfs(root, ans);
        return ans;
    }
};
```