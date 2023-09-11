# Group the People Given the Group Size They Belong To

https://leetcode.com/problems/group-the-people-given-the-group-size-they-belong-to/description

There are n people that are split into some unknown number of groups. Each person is labeled with a unique ID from 0 to n - 1.

You are given an integer array groupSizes, where groupSizes[i] is the size of the group that person i is in. For example, if groupSizes[1] = 3, then person 1 must be in a group of size 3.

Return a list of groups such that each person i is in a group of size groupSizes[i].

Each person should appear in exactly one group, and every person must be in a group. If there are multiple answers, return any of them. It is guaranteed that there will be at least one valid solution for the given input.

## Approach 1

``` C++
    vector<vector<int>> groupThePeople(vector<int>& groupSizes) {
        std::unordered_map<int, std::vector<int>> ppl; // size - IDs

        for (int i = 0; i < groupSizes.size(); i++)
        {
           ppl[groupSizes[i]].emplace_back(i);
        }

        std::vector<std::vector<int>> ans;
        for (auto& [size, idx] : ppl)
        {
            while (!idx.empty())
            { // Assemble the group
                std::vector<int> temp(size);
                for (int i = 0; i < size; i++)
                { // Order doesn't matter
                    temp[i] = idx.back();
                    idx.pop_back();                   
                }
                ans.emplace_back(temp);
                /* 
                // Second way: 
                std::vector<int> temp(idx.begin(), idx.begin() + size);
                ans.emplace_back(temp);
                idx.erase(idx.begin(), idx.begin() + size);
                */

            }
        }
        return ans;
    }
```

## Approach 2

``` C++
    vector<vector<int>> groupThePeople(vector<int>& groupSizes) {
        std::unordered_map<int, std::vector<int>> ppl; // size - IDs

        std::vector<std::vector<int>> ans;

        for (int i = 0; i < groupSizes.size(); i++)
        {
            ppl[groupSizes[i]].emplace_back(i);

            if (ppl[groupSizes[i]].size() == groupSizes[i])
            { // If the group can be made, add it to the ans and reset the container.
                ans.emplace_back(ppl[groupSizes[i]]);
                ppl[groupSizes[i]].clear();
            }
        }

        return ans;
    }
```