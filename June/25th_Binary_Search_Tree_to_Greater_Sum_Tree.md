# Binary Search Tree to Greater Sum Tree

https://leetcode.com/problems/binary-search-tree-to-greater-sum-tree


Given the root of a Binary Search Tree (BST), convert it to a Greater Tree such that every key of the original BST is changed to the original key plus the sum of all keys greater than the original key in BST.


## Approach 

``` C++
    int postOrder(TreeNode* node, int& sum)
    {
        if (!node)
        {
            return 0;
        }
        postOrder(node->right, sum);
        node->val += sum;
        sum = node->val;
        postOrder(node->left, sum);
        return sum;
    }

    TreeNode* bstToGst(TreeNode* root) {
        int sum = 0;
        postOrder(root, sum);
        return root;
    }
```

``` JavaScript
var bstToGst = function(root) {
    var sum = 0;
    const postOrder = (root) => {
        if (!root) {
            return;
        }
        postOrder(root.right);
        root.val += sum;
        sum = root.val;
        postOrder(root.left);
    }
    postOrder(root);
    return root;
};
```