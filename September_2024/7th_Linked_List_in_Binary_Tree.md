Linked List in Binary Tree

https://leetcode.com/problems/linked-list-in-binary-tree

Given a binary tree root and a linked list with head as the first node. 

Return True if all the elements in the linked list starting from the head correspond to some downward path connected in the binary tree otherwise return False.

In this context downward path means a path that starts at some node and goes downwards.

## Appraoch 

Recursive
``` C++
    bool isSub(ListNode* curr, TreeNode* treeNode)
    {
        if (!curr) return true; 
        if (!treeNode) return false;

        if (curr->val == treeNode->val)
        {
            return isSub(curr->next, treeNode->left) || isSub(curr->next, treeNode->right);
        }
        return false;
    }

    bool isSubPath(ListNode* head, TreeNode* root) {
        if (!root)
        {
            return false;
        }
        return isSub(head, root) || isSubPath(head, root->left) || isSubPath(head, root->right);
    }
```

Iterative
``` C++
    bool isSub(ListNode* curr, TreeNode* treeNode)
    {
        if (!curr) return true; 
        if (!treeNode) return false;

        if (curr->val == treeNode->val)
        {
            return isSub(curr->next, treeNode->left) || isSub(curr->next, treeNode->right);
        }
        return false;
    }

    bool isSubPath(ListNode* head, TreeNode* root) {
        std::stack<TreeNode*> st;
        st.emplace(root);
        while (!st.empty())
        {
            TreeNode* curr= st.top();
            st.pop();
            if (isSub(head, curr)) return true;
            if (curr->left) st.emplace(curr->left);
            if (curr->right) st.emplace(curr->right);
        }
        return false;
    }
```