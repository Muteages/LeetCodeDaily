# Evaluate Boolean Binary Tree

https://leetcode.com/problems/evaluate-boolean-binary-tree

You are given the root of a full binary tree with the following properties:

Leaf nodes have either the value 0 or 1, where 0 represents False and 1 represents True.
Non-leaf nodes have either the value 2 or 3, where 2 represents the boolean OR and 3 represents the boolean AND.
The evaluation of a node is as follows:

If the node is a leaf node, the evaluation is the value of the node, i.e. True or False.
Otherwise, evaluate the node's two children and apply the boolean operation of its value with the children's evaluations.
Return the boolean result of evaluating the root node.


## Approach 

``` C++
    bool evaluateTree(TreeNode* root) {
        if (!root->left && !root->right)
        { // Leaf node
            return root->val;
        }

        bool left = evaluateTree(root->left);
        bool right = evaluateTree(root->right);
        return root->val == 2 ? left | right : left & right;
    }
```

