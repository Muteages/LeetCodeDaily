# Find Players With Zero or One Losses

https://leetcode.com/problems/find-players-with-zero-or-one-losses

You are given an integer array matches where matches[i] = [winneri, loseri] indicates that the player winneri defeated player loseri in a match.

Return a list answer of size 2 where:

answer[0] is a list of all players that have not lost any matches.
answer[1] is a list of all players that have lost exactly one match.
The values in the two lists should be returned in increasing order.

## Approach 

``` C++
    vector<vector<int>> findWinners(vector<vector<int>>& matches) {
        std::unordered_map<int, int> loseCount; 
        for (const auto& match : matches)
        {
            if (loseCount.find(match[0]) == loseCount.end())
            { // Add new player into hash map
                loseCount[match[0]] = 0;
            }
            loseCount[match[1]]++;
        }

        std::vector<std::vector<int>> ans(2);
        for (const auto& [player, lose] : loseCount)
        {
            if (lose == 0)
            { // Not lost any matches
                ans[0].emplace_back(player);
            }
            else if (lose == 1)
            { // Lost one match
                ans[1].emplace_back(player);
            }
        }
        std::sort(ans[0].begin(), ans[0].end());
        std::sort(ans[1].begin(), ans[1].end());
        return ans;
    }
```