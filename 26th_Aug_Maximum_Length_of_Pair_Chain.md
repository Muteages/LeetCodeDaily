# Maximum Length of Pair Chain

https://leetcode.com/problems/maximum-length-of-pair-chain/description/

You are given an array of n pairs pairs where pairs[i] = [lefti, righti] and lefti < righti.

A pair p2 = [c, d] follows a pair p1 = [a, b] if b < c. A chain of pairs can be formed in this fashion.

Return the length longest chain which can be formed.


## Approach

``` C++
    int findLongestChain(vector<vector<int>>& pairs) {
        std::sort(pairs.begin(), pairs.end(), 
        [](std::vector<int>& v1, std::vector<int>& v2)
        { // According to the right element
            return v1[1] < v2[1];
        });

        int prevRight = INT_MIN;
        int cnt = 0;
        for (const auto& pair : pairs)
        {
            if (pair[0] > prevRight)
            {
                cnt++;
                prevRight = pair[1];
            }
        }   
        return cnt;
    }
```