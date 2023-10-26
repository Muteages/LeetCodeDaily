# Binary Trees with Factors

https://leetcode.com/problems/binary-trees-with-factors

Given an array of unique integers, arr, where each integer arr[i] is strictly greater than 1.

We make a binary tree using these integers, and each number may be used for any number of times. Each non-leaf node's value should be equal to the product of the values of its children.


## Approach 

``` C++
    int mod = 1e9 + 7;
    int numFactoredBinaryTrees(vector<int>& arr) {
        std::sort(arr.begin(), arr.end());
        std::unordered_map<int, long> treeCnt; // node - treeNum with the current node as root
        treeCnt[arr[0]] = 1;
        int res = 1;

        for (int i = 1; i < arr.size(); i++)
        {
            int curr = arr[i];
            long tempCnt = 1; // self
            for (auto& [node, cnt] : treeCnt)
            {
                if (curr % node == 0 && treeCnt.find(curr / node) != treeCnt.end())
                { // Find the factor
                    tempCnt += treeCnt[node] * treeCnt[curr / node];
                }
            }
            treeCnt[curr] = tempCnt;
            res = (res + tempCnt) % mod;
        }
        return res;
    }
```