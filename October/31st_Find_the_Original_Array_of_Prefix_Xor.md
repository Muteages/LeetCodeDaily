# Find the Original Array of Prefix Xor

https://leetcode.com/problems/find-the-original-array-of-prefix-xor

You are given an integer array pref of size n. Find and return the array arr of size n that satisfies:

pref[i] = arr[0] ^ arr[1] ^ ... ^ arr[i].
Note that ^ denotes the bitwise-xor operation.


## Approach 
``` C++
    vector<int> findArray(vector<int>& pref) {
        std::vector<int> ans(pref.size(), pref[0]);
        for (int i = 1; i < pref.size(); i++)
        {
            ans[i] = pref[i] ^ pref[i - 1];
        }
        return ans;
    }
```