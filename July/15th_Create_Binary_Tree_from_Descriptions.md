# Create Binary Tree from Descriptions

https://leetcode.com/problems/create-binary-tree-from-descriptions

You are given a 2D integer array descriptions where descriptions[i] = [parenti, childi, isLefti] indicates that parenti is the parent of childi in a binary tree of unique values. Furthermore,

If isLefti == 1, then childi is the left child of parenti.
If isLefti == 0, then childi is the right child of parenti.
Construct the binary tree described by descriptions and return its root.

The test cases will be generated such that the binary tree is valid.


## Aprroach 1

``` C++
    TreeNode* createBinaryTree(vector<vector<int>>& descriptions) {
        std::unordered_map<int, TreeNode*> nodes;
        std::unordered_set<int> children;
        int parent{}, child{};
        bool isLeft{};
        for (const auto& des : descriptions)
        {
            parent = des[0];
            child = des[1];
            isLeft = des[2];
            if (!nodes.count(parent))
            {
                nodes[parent] = new TreeNode(parent);
            }
            if (!nodes.count(child))
            {
                nodes[child] = new TreeNode(child);
            }
            children.insert(child);
            if (isLeft)
            {
                nodes[parent]->left = nodes[child];
            }
            else 
            {
                nodes[parent]->right = nodes[child];
            }
        }
        // Find the root
        for (const auto& [v, p] : nodes)
        {
            if (!children.count(v))
            {
                return p;
            }
        }
        return nullptr;
    }
```

``` JavaScript
var createBinaryTree = function(descriptions) {
    let nodes = new Map();
    let children = new Set();
    
    for (let [parent, child, isLeft] of descriptions) {
        if (!nodes.has(parent)) {
            nodes.set(parent, new TreeNode(parent));
        }
        if (!nodes.has(child)) {
            nodes.set(child, new TreeNode(child));
        }
        
        children.add(child);
        
        if (isLeft) {
            nodes.get(parent).left = nodes.get(child);
        } else {
            nodes.get(parent).right = nodes.get(child);
        }
    }

    for (let node of nodes.keys()) {
        if (!children.has(node)) {
            return nodes.get(node);
        }
    }
    
    return null;
};
```

