# Same Tree

Given the roots of two binary trees p and q, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical, and the nodes have the same value.

## Approach 1

Recursive 
``` C++
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if (!p && !q)
        {
            return true;
        }
        if (!p || !q || p->val != q->val)
        {
            return false;
        }
        bool left = isSameTree(p->left, q->left);
        bool right = isSameTree(p->right, q->right);
        return left && right;
    }
```

## Approach 2

Iterative

``` C++
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if (!p && !q)
        {
            return true;
        }
        if (!p || !q)
        {
            return false;
        }

        std::queue<TreeNode*> bfs;
        bfs.emplace(p);
        bfs.emplace(q);
        while (!bfs.empty())
        {
            auto p1 = bfs.front();
            bfs.pop();
            auto p2 = bfs.front();
            bfs.pop();
            if (!p1 && !p2)
            {
                continue;
            }
            if (!p1 || !p2 || p1->val != p2->val)
            {
                return false;
            }
            bfs.emplace(p1->left);
            bfs.emplace(p2->left);
            bfs.emplace(p1->right);
            bfs.emplace(p2->right);
        }
        return true;
    }
```