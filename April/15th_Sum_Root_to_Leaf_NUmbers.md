# Sum Root to Leaf Numbers

https://leetcode.com/problems/sum-root-to-leaf-numbers

You are given the root of a binary tree containing digits from 0 to 9 only.

Each root-to-leaf path in the tree represents a number.

For example, the root-to-leaf path 1 -> 2 -> 3 represents the number 123.

## Approach 1

``` C++
    int dfs(TreeNode* node, int value)
    {
        if (!node)
        {
            return 0;
        }
        value = value * 10 + (node ? node->val : 0);
        if (node && !node->left && !node->right)
        { // Find a leaf node
            return value;
        }
        return dfs(node->left, value)+ dfs(node->right, value);
    }

    int sumNumbers(TreeNode* root) {
        return dfs(root, 0);
    }
```

## Approach 2

``` C++
    int sum = 0;
    void dfs(TreeNode* node, int value)
    {
        if (!node)
        {
            return;
        }
        value = value * 10 + node->val;
        if (!node->left && !node->right)
        { // Leaf node
            sum += value;
        }
        dfs(node->left, value);
        dfs(node->right, value);
    }

    int sumNumbers(TreeNode* root) {
        dfs(root, 0);
        return sum;
    }
```

## Approach 3

Iterative dfs

``` C++
    int sumNumbers(TreeNode* root) {
        int sum = 0;
        std::stack<std::pair<TreeNode*, int>> st;
        st.emplace(root, 0);
        while (!st.empty())
        {
            auto [node, value] = st.top();
            st.pop();
            value = value * 10 + node->val;
            if (!node->left && !node->right)
            {
                sum += value;
                continue;
            }
            if (node->left)
            {
                st.emplace(node->left, value);
            }
            if (node->right)
            {
                st.emplace(node->right, value);
            }
        }
        return sum;
    }
```