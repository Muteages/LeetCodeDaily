# Balance a Binary Search Tree

https://leetcode.com/problems/balance-a-binary-search-tree

Given the root of a binary search tree, return a balanced binary search tree with the same node values. If there is more than one answer, return any of them.



## Approach 

``` JavaScript
var balanceBST = function(root) {
    let sorted = [];
    const inOrder = (root) => {
        if (!root) {
            return null;
        }
        inOrder(root.left);
        sorted.push(root);
        inOrder(root.right);
    }
    const balanceTree = (l, r) => {
        if (l > r) {
            return null;
        }  
        let m = Math.floor((l + r) / 2);  
        sorted[m].left = balanceTree(l, m - 1);
        sorted[m].right = balanceTree(m + 1, r);
        return sorted[m];
    };

    inOrder(root);
    return balanceTree(0, sorted.length - 1);
};
```

``` C++
    vector<TreeNode*> sorted;
    void inOrder(TreeNode* node)
    {
        if (!node)
        {
            return;
        }
        inOrder(node->left);
        sorted.emplace_back(node);
        inOrder(node->right);
    }

    TreeNode* balanceTree(int l, int r)
    {
        if (l > r)
        {
            return nullptr;
        }
        int m = (l + r) / 2;
        sorted[m]->left = balanceTree(l, m - 1);
        sorted[m]->right = balanceTree(m + 1, r);
        return sorted[m];
    }

    TreeNode* balanceBST(TreeNode* root) {
        inOrder(root);
        return balanceTree(0, sorted.size() - 1);
    }
```

 