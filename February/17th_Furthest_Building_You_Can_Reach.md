# Furthest Building You Can Reach

https://leetcode.com/problems/furthest-building-you-can-reach

You are given an integer array heights representing the heights of buildings, some bricks, and some ladders.

You start your journey from building 0 and move to the next building by possibly using bricks or ladders.

While moving from building i to building i+1 (0-indexed),

If the current building's height is greater than or equal to the next building's height, you do not need a ladder or bricks.
If the current building's height is less than the next building's height, you can either use one ladder or (h[i+1] - h[i]) bricks.
Return the furthest building index (0-indexed) you can reach if you use the given ladders and bricks optimally.

## Approach 1

Greedily use ladders first and if ladders are used up, use bricks for the least gap.

``` C++
    int furthestBuilding(vector<int>& heights, int bricks, int ladders) {
        int n = heights.size();
        std::priority_queue<int, std::vector<int>, std::greater<int>> gaps;
        for (int i = 0; i < n - 1; i++)
        {
            int gap = heights[i + 1] - heights[i];

            if (gap <= 0)
            { // No need to use bricks or ladders
                continue;
            }
            
            gaps.emplace(gap); // Try to use ladders first
            if (gaps.size() > ladders)
            { // If ladders are used up, select the minimum gap and use bricks instead
                bricks -= gaps.top();
                gaps.pop();
            }

            if (bricks < 0)
            { // Can't go further
                return i;
            }
        }
        return n - 1;
    }
```


## Approach 2

Greedily use bricks first and if bricks are used up, use a ladder for the largest gap. 

``` C++
    int furthestBuilding(vector<int>& heights, int bricks, int ladders) {
        int n = heights.size();
        if (ladders >= n - 1)
        {
            return n - 1;
        }
        std::priority_queue<int> gaps;
        for (int i = 0; i < n - 1; i++)
        {
            int gap = heights[i + 1] - heights[i];
            if (gap <= 0)
            { // Doesn't need bricks or ladders
                continue;
            }

            if (bricks >= gap)
            { // Use bricks first
                bricks -= gap;
                gaps.emplace(gap);
            }
            else if (ladders)
            {
                if (!gaps.empty() && gaps.top() > gap)
                { // Update bricks and gaps container if we can replace the longest gap with one ladder
                    bricks += gaps.top() - gap;
                    gaps.pop();
                    gaps.emplace(gap);
                }
                ladders--;
            }
            else
            { // There aren't enough ladder or bricks to go further
                return i;
            }
        }
        return n - 1;
    }
```




