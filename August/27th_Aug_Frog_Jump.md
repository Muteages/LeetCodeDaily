# Frog Jump

https://leetcode.com/problems/frog-jump/description/

A frog is crossing a river. The river is divided into some number of units, and at each unit, there may or may not exist a stone. The frog can jump on a stone, but it must not jump into the water.

Given a list of stones' positions (in units) in sorted ascending order, determine if the frog can cross the river by landing on the last stone. Initially, the frog is on the first stone and assumes the first jump must be 1 unit.

If the frog's last jump was k units, its next jump must be either k - 1, k, or k + 1 units. The frog can only jump in the forward direction.


## Approach 

Use unordered_map to store the current position and the possible next steps. i.e k-1, k, k+1. Update all stones from the first stone and see if the last stone is reachable.


``` C++
   bool canCross(vector<int>& stones) {

        if (stones[1] != 1)
        { // The first step must be 1 unit
            return false;
        }

        std::unordered_map<int, std::unordered_set<int>> ump; // current position - {possible jump steps}

        ump[stones[1]].insert(1); // The first step

        for (int i = 1; i < stones.size(); i++)
        {
            for (auto& jump : ump[stones[i]])
            { // Update three possible steps:
                ump[stones[i] + jump - 1].insert(jump - 1);
                ump[stones[i] + jump].insert(jump);
                ump[stones[i] + jump + 1].insert(jump + 1);
            }
        }

        return ump[stones.back()].size() != 0;
    }
```