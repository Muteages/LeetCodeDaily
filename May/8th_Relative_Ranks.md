# Relative Ranks

https://leetcode.com/problems/relative-ranks

You are given an integer array score of size n, where score[i] is the score of the ith athlete in a competition. All the scores are guaranteed to be unique.

The athletes are placed based on their scores, where the 1st place athlete has the highest score, the 2nd place athlete has the 2nd highest score, and so on. The placement of each athlete determines their rank:

The 1st place athlete's rank is "Gold Medal".
The 2nd place athlete's rank is "Silver Medal".
The 3rd place athlete's rank is "Bronze Medal".
For the 4th place to the nth place athlete, their rank is their placement number (i.e., the xth place athlete's rank is "x").
Return an array answer of size n where answer[i] is the rank of the ith athlete.



## Approach 

``` C++
    vector<string> findRelativeRanks(vector<int>& score) {
        std::priority_queue<std::pair<int, int>> pq; // score - index
        int n = score.size();
        for (int i = 0; i < n; i++)
        {
            pq.emplace(score[i], i);
        }

        std::vector<std::string> ans(n);
        const std::vector<std::string> medals = {"Gold Medal", "Silver Medal", "Bronze Medal"};
        for (int i = 1; i <= n; i++)
        {            
            std::string rank{};
            if (i > 3)
            {
                rank = std::to_string(i);
            }
            else
            {
                rank = medals[i - 1];
            }
            int idx = pq.top().second;
            pq.pop();
            ans[idx] = std::move(rank);
        }
        return ans;
    }
```