# Find the Town Judge

https://leetcode.com/problems/find-the-town-judge

In a town, there are n people labeled from 1 to n. There is a rumor that one of these people is secretly the town judge.

If the town judge exists, then:

The town judge trusts nobody.
Everybody (except for the town judge) trusts the town judge.
There is exactly one person that satisfies properties 1 and 2.
You are given an array trust where trust[i] = [ai, bi] representing that the person labeled ai trusts the person labeled bi. If a trust relationship does not exist in trust array, then such a trust relationship does not exist.

Return the label of the town judge if the town judge exists and can be identified, or return -1 otherwise.

## Approach

``` C++
    int findJudge(int n, vector<vector<int>>& trust) {
        std::vector<int> trusted(1001, 0), trusts(1001, 0);
        for (const auto& t : trust)
        {
            trusted[t[1]]++; // in dergree
            trusts[t[0]] = t[1]; // out dergree
        }

        for (int i = 1; i < 1001; i++)
        {
            if (trusted[i] == n - 1 && trusts[i] == 0)
            {
                return i;
            }
        }
        return -1;
    }
```
