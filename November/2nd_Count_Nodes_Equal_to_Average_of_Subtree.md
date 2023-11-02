# Count Nodes Equal to Average of Subtree

https://leetcode.com/problems/count-nodes-equal-to-average-of-subtree

Given the root of a binary tree, return the number of nodes where the value of the node is equal to the average of the values in its subtree.


## Approach 1

``` C++
    int ans = 0;
    std::tuple<int, int>parseSubtree(TreeNode* node) // sum - subtree node count
    {
        if (!node)
        {
            return {0, 0};
        }
        auto [leftSum, leftCount] = parseSubtree(node->left);
        auto [rightSum, rightCount] = parseSubtree(node->right);
        int sum = node->val + leftSum + rightSum;
        int count = 1 + leftCount + rightCount;
        if (sum / count == node->val)
        {
            ans++;
        }
        return {sum, count};
    }

    int averageOfSubtree(TreeNode* root) {
        parseSubtree(root);
        return ans;
    }
```
