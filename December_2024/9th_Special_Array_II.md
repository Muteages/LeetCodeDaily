# Special Array II 

https://leetcode.com/problems/special-array-ii

An array is considered special if every pair of its adjacent elements contains two numbers with different parity.

You are given an array of integer nums and a 2D integer matrix queries, where for queries[i] = [fromi, toi] your task is to check that 
subarray
 nums[fromi..toi] is special or not.

Return an array of booleans answer such that answer[i] is true if nums[fromi..toi] is special.

 
## Approach 

Prefix

``` C++
    vector<bool> isArraySpecial(vector<int>& nums, vector<vector<int>>& queries) {
        const int n = nums.size();
        std::vector<int> prefix(n, 0); // Record the number of current non-special pairs

        for (int i = 1; i < n; i++)
        {
            prefix[i] = prefix[i - 1];
            if ((nums[i - 1] & 1) == (nums[i] & 1))
            { // Encounter a non-special pair, i.e the adjacent elements have the same parity
                prefix[i]++;
            }
        }

        std::vector<bool> specialPairs;
        specialPairs.reserve(queries.size());
        for (const auto& q : queries)
        {
            int l = q[0], r = q[1];
            specialPairs.emplace_back(prefix[l] == prefix[r]); // if p[l] == p[r], then subarray is special
        }
        return specialPairs;
    }
```

``` JavaScript
var isArraySpecial = function(nums, queries) {
    const n = nums.length;
    let prefix = new Array(n).fill(0);
    for (let i = 1; i < n; i++) {
        prefix[i] = prefix[i - 1] + ((nums[i - 1] & 1) === (nums[i] & 1));
    }
    return queries.map(([l ,r]) => prefix[l] == prefix[r]);
    /*
    let specialPairs = [];
    for (const [l, r] of queries) {
        specialPairs.push(prefix[l] == prefix[r]);
    }
    return specialPairs;
    */
};
```