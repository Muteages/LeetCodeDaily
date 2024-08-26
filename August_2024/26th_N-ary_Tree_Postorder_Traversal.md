# N-ary Tree Postorder Traversal


## Approach 1

Recursive approach

``` JavaScript
var postorder = function(root) {
    let ans = [];
    const post = (node) => {
        if (!node) return ans;
        for (let child of node.children) {
            post(child);
        }
        ans.push(node.val);
    }
    post(root);
    return ans;
};
```

## Approach 2

Iterative approach

``` JavaScript
var postorder = function(root) {
    if (!root) return [];
    const ans = [], st = [root];
    while (st.length) {
        let curr = st.pop();
        ans.push(curr.val);
        st.push(...curr.children);
    }
    return ans.reverse();
};
```