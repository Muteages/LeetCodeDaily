# Sum of Left Leaves

Given the root of a binary tree, return the sum of all left leaves.

## Approach 1

Iterative dfs

``` C++
    int sumOfLeftLeaves(TreeNode* root) {
        std::stack<std::pair<TreeNode*, bool>> st;
        st.emplace(root, false);
        int sum = 0;
        while (!st.empty())
        {
            auto [node, isLeft] = st.top();
            st.pop();
            if (!node->left && !node->right && isLeft)
            {
                sum += node->val;
            }
            if (node->left)
            {
                st.emplace(node->left, 1);
            }
            if (node->right)
            {
                st.emplace(node->right, 0);
            }
        }
        return sum;
    }
```

## Approach 2

Recursive 

``` C++
    int sumOfLeftLeaves(TreeNode* root) {
        if (!root)
        {
            return 0;
        }
        int sum = 0;
        if (root->left && !root->left->left && !root->left->right)
        { // Find a left leaf
            sum += root->left->val;
        }
        sum += sumOfLeftLeaves(root->left) + sumOfLeftLeaves(root->right);
        return sum;
    }
```

