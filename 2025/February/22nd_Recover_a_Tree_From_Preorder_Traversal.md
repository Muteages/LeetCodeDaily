# Recover a Tree From Preorder Traversal

https://leetcode.com/problems/recover-a-tree-from-preorder-traversal

We run a preorder depth-first search (DFS) on the root of a binary tree.

At each node in this traversal, we output D dashes (where D is the depth of this node), then we output the value of this node.  If the depth of a node is D, the depth of its immediate child is D + 1.  The depth of the root node is 0.

If a node has only one child, that child is guaranteed to be the left child.

Given the output traversal of this traversal, recover the tree and return its root.

## Approach 

Iteration

``` C++
    inline int getDepth(std::string& t, int& idx)
    {
        int depth = 0;
        int n = t.size();
        while (idx < n && t[idx] == '-')
        {
            depth++;
            idx++;
        }
        return depth;
    }

    inline int getNum(std::string& t, int& idx)
    {
        int num = 0;
        int n = t.size();
        while (idx < n && std::isdigit(t[idx]))
        {
            num = num * 10 + (t[idx++] - '0');
        }
        return num;
    }


    TreeNode* recoverFromPreorder(string& traversal) {
        int idx = 0, n = traversal.size();
        // Find root first
        int num = getNum(traversal, idx);
        TreeNode* root = new TreeNode(num);
        int depth = 0;

        std::vector<std::pair<TreeNode*, int>> node2Depth{};
        node2Depth.emplace_back(root, depth);

        while (idx < n)
        {
            // Calculate current num and depth
            depth = getDepth(traversal, idx);
            num = getNum(traversal, idx);
            TreeNode* curr = new TreeNode(num);

            while (node2Depth.back().second != depth - 1)
            {
                node2Depth.pop_back();
            }
            auto& [pn, _] = node2Depth.back();
            if (!pn->left)
            {
                pn->left = curr;
            }
            else
            {
                pn->right = curr;
            }

            node2Depth.emplace_back(curr, depth);
        }

        return root;
    }
```

``` Python
    def recoverFromPreorder(self, traversal: str) -> Optional[TreeNode]:
        root = None
        i = 0
        n = len(traversal)
        st = []
        while i < n:
            # Get depth
            depth = 0
            while i < n and traversal[i] == '-':
                depth += 1
                i += 1
            
            # Get number
            num = 0
            while i < n and traversal[i].isdigit():
                num = num * 10 + int(traversal[i])
                i += 1
            
            node = TreeNode(num)
            if depth == 0:
                root = node
            else:
                while st[-1][1] != (depth - 1):
                    st.pop()

                if st[-1][0].left is None:
                    st[-1][0].left = node
                else:
                    st[-1][0].right = node

            st.append([node, depth])
        
        return root
```

## Approach 2

Recursion

``` JavaScript
var recoverFromPreorder = function(t) {
    let i = 0;
    const n = t.length;

    const dfs = (depth) => {
        // Get current depth
        let d = 0;
        while (i < n && t[i] === '-') {
            d++;
            i++;
        }

        if (d < depth) {
            i -= d;
            return null;
        }
        // Get number
        let num = 0;
        while (i < n && !isNaN(t[i])) {
            num = num * 10 + Number(t[i]);
            i++;
        }

        let node = new TreeNode(num);
        node.left = dfs(depth + 1);
        node.right = dfs(depth + 1);
        return node;
    }
    
    return dfs(0);
};
```

