# XOR Queries of a Subarray

https://leetcode.com/problems/xor-queries-of-a-subarray

You are given an array arr of positive integers. You are also given the array queries where queries[i] = [lefti, righti].

For each query i compute the XOR of elements from lefti to righti (that is, arr[lefti] XOR arr[lefti + 1] XOR ... XOR arr[righti] ).

Return an array answer where answer[i] is the answer to the ith query.

## Approach 

``` C++
    vector<int> xorQueries(vector<int>& arr, vector<vector<int>>& queries) {
        int n = queries.size();
        std::vector<int> ans(n);
        //std::partial_sum(arr.begin(), arr.end(), arr.begin(), std::bit_xor<int>());
        for (int i = 1; i < arr.size(); i++)
        {
            arr[i] ^= arr[i - 1];
        }
        for (int i = 0; i < n; i++)
        {
            int st = queries[i][0], end = queries[i][1];
            ans[i] = st == 0 ? arr[end] : (arr[end] ^ arr[st - 1]);  
        }
        return ans;
    }
```