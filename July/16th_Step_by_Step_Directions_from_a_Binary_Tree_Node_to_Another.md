# Step by Step Directions from a Binary Tree Node to Another

https://leetcode.com/problems/step-by-step-directions-from-a-binary-tree-node-to-another

You are given the root of a binary tree with n nodes. Each node is uniquely assigned a value from 1 to n. You are also given an integer startValue representing the value of the start node s, and a different integer destValue representing the value of the destination node t.

Find the shortest path starting from node s and ending at node t. Generate step-by-step directions of such path as a string consisting of only the uppercase letters 'L', 'R', and 'U'. Each letter indicates a specific direction:

'L' means to go from a node to its left child node.
'R' means to go from a node to its right child node.
'U' means to go from a node to its parent node.
Return the step-by-step directions of the shortest path from node s to node t.

## Approach 

``` C++
    string getDirections(TreeNode* root, int startValue, int destValue) {
        root = getLCA(root, startValue, destValue);
        std::string st{}, dest{};
        dfs(root, st, startValue);
        dfs(root, dest, destValue);
        int n = st.length();
        return std::string(n, 'U') + dest;
    }
    
    TreeNode* getLCA(TreeNode* node, int st, int dest)
    {
        if (!node || node->val == st || node->val == dest)
        {
            return node;
        }
        TreeNode* left = getLCA(node->left, st, dest);
        TreeNode* right = getLCA(node->right, st, dest);
        if (!left)
        {
            return right;
        }
        else if (!right)
        {
            return left;
        }
        return node;
    }

    bool dfs(TreeNode* node, std::string& s, int target)
    {
        if (!node)
        {
            return 0;
        }
        if (node->val == target)
        {
            return 1;
        }
        s += 'L';
        if (dfs(node->left, s, target))
        {
            return 1;
        }
        s.pop_back();

        s += 'R';
        if (dfs(node->right, s, target))
        {
            return 1;
        }
        s.pop_back();
        return 0;
    }

```
