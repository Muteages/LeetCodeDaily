# Delete Node in a BST

https://leetcode.com/problems/delete-node-in-a-bst/description/

Given a root node reference of a BST and a key, delete the node with the given key in the BST. Return the root node reference (possibly updated) of the BST.

## Apporach
Basically there are three cases:
    - Target node is a leaf
    - Target node has only one child
    - Target node has two children

``` C++
   TreeNode* deleteNode(TreeNode* root, int key) {
        if (!root)
        {
            return nullptr;
        }

        /* 1. If the target node doesn't have any child node, just remove it
           2. If the target node has only one child, replace target node with it's child.
           3. If the target node has both left and right children, find the rightmost node in its left subtree 
           and replace the target with it  
        */

        // DFS
        if (root->val < key)
        {
            root->right = deleteNode(root->right, key);
        }
        else if (root->val > key)
        {
            root->left = deleteNode(root->left, key);
        }
        else 
        { // Find the target node
            if (!root->right && !root->left)
            { // No child
                delete root;
                root = nullptr;
                return root;
            }

            else if (!root->right || !root->left)
            { // only one child
                TreeNode* subTree = root->left? root->left : root->right;
                delete root;
                root = nullptr;
                return subTree;
            }

            else
            {   // two children
                TreeNode* rightmost = root->left;
                while (rightmost->right)
                {
                    rightmost = rightmost->right;
                }
                root->val = rightmost->val;
                root->left = deleteNode(root->left, rightmost->val);
            }

        }
        return root;
    }
```