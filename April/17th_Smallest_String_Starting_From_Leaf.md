# Smallest String Starting From Leaf

https://leetcode.com/problems/smallest-string-starting-from-leaf

You are given the root of a binary tree where each node has a value in the range [0, 25] representing the letters 'a' to 'z'.

Return the lexicographically smallest string that starts at a leaf of this tree and ends at the root.

As a reminder, any shorter prefix of a string is lexicographically smaller.


## Approach 1

Recursive dfs

``` C++
    std::deque<char> ans = {'a' + 26};

    void dfs(TreeNode* node, std::deque<char>& curr)
    {
        if (!node)
        {
            return;
        }
        curr.emplace_front(node->val + 'a');
        if (!node->left && !node->right)
        {
            ans = std::min(ans, curr);
        }
        dfs(node->left, curr);
        dfs(node->right, curr);
        curr.pop_front();
    }

    string smallestFromLeaf(TreeNode* root) {
        std::deque<char> curr;
        dfs(root, curr);
        return std::string(ans.begin(), ans.end());
    }
```

## Approach 2

Iterative dfs

``` C++
    string smallestFromLeaf(TreeNode* root) {
        std::string ans = {26 + 'a'};
        std::stack<std::pair<TreeNode*, std::string>> st;
        st.emplace(root, "");
        std::string temp{};
        while (!st.empty())
        {
            auto [node, prevS] = st.top();
            st.pop();
            prevS += node->val + 'a';
            if (!node->left && !node->right)
            {
                temp = std::move(prevS);
                std::reverse(temp.begin(), temp.end());
                ans = std::min(ans, temp);
            }
            if (node->left)
            {
                st.emplace(node->left, prevS);
            }
            if (node->right)
            {
                st.emplace(node->right, prevS);
            }
        }
        return ans;
    }
```