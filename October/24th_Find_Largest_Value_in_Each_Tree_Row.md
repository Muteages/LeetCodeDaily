# Find Largest Value in Each Tree Row

https://leetcode.com/problems/find-largest-value-in-each-tree-row

Given the root of a binary tree, return an array of the largest value in each row of the tree (0-indexed).

## Approach 

``` C++
    vector<int> largestValues(TreeNode* root) {
        if (!root)
        {
            return {};
        }
        std::vector<int> ans;
        std::queue<TreeNode*> q;
        q.emplace(root);
        int curMax = INT_MIN;
        int totalNode = 1;
        int visited = 0;
        while (!q.empty())
        {
            visited++;
            TreeNode* curr = q.front();
            q.pop();
            curMax = std::max(curMax, curr->val);
            if (curr->left)
            {
                q.emplace(curr->left);
            }
            if (curr->right)
            {
                q.emplace(curr->right);
            }

            if (visited == totalNode)
            {
                ans.emplace_back(curMax);
                curMax = INT_MIN;

                visited = 0;
                totalNode = q.size();
            }
        }
        return ans;
    }
```