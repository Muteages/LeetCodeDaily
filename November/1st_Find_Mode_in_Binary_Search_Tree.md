# Find Mode in Binary Search Tree

https://leetcode.com/problems/find-mode-in-binary-search-tree

Given the root of a binary search tree (BST) with duplicates, return all the mode(s) (i.e., the most frequently occurred element) in it.

If the tree has more than one mode, return them in any order.

## Approach 1

``` C++
    vector<int> findMode(TreeNode* root) {
        std::vector<int> ans;
        std::unordered_map<int, int> frequency; // val - frequency
        std::queue<TreeNode*> bfs;
        bfs.emplace(root);
        while (!bfs.empty())
        {
            TreeNode* curr = bfs.front();
            bfs.pop();
            frequency[curr->val]++;
            if (curr->left)
            {
                bfs.emplace(curr->left);
            }
            if (curr->right)
            {
                bfs.emplace(curr->right);
            }
        }

        int maxCnt = 0;
        for (auto& [val, freq] : frequency)
        {
            if (freq > maxCnt)
            {
                maxCnt = freq;
                ans.clear();
                ans.emplace_back(val);
            }
            else if (freq == maxCnt)
            {
                ans.emplace_back(val);
            }
        }

        return ans;
    }
```

## Approach 2

Without using any extra space

``` C++
   std::vector<int> ans;
    int maxCount = 0;
    int curCount = 0;
    int prevVal = INT_MIN;
    void inOrder(TreeNode* node)
    {
        if (!node)
        {
            return;
        }
        // In-order
        inOrder(node->left);

        if (node->val == prevVal)
        {
            curCount++;
        }
        else
        {
            prevVal = node->val;
            curCount = 1;
        }

        if (curCount > maxCount)
        {
            maxCount = curCount;
            ans.clear();
            ans.emplace_back(node->val);
        }
        else if (curCount == maxCount)
        {
            ans.emplace_back(node->val);
        }
        inOrder(node->right);
    }
    vector<int> findMode(TreeNode* root) {
        inOrder(root);
        return ans;
    }
```