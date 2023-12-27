# Minimum Time to Mkae Rope Colourful

https://leetcode.com/problems/minimum-time-to-make-rope-colorful

Alice has n balloons arranged on a rope. You are given a 0-indexed string colors where colors[i] is the color of the ith balloon.

Alice wants the rope to be colorful. She does not want two consecutive balloons to be of the same color, so she asks Bob for help. Bob can remove some balloons from the rope to make it colorful. You are given a 0-indexed integer array neededTime where neededTime[i] is the time (in seconds) that Bob needs to remove the ith balloon from the rope.

Return the minimum time Bob needs to make the rope colorful.

## Approach 

``` C++
    int minCost(string colors, vector<int>& neededTime) {
        int ans = 0;
        for (int i = 1; i < colors.length(); i++)
        {
            if (colors[i] == colors[i - 1])
            { // Find the balloon having the same colour with the previous one
                ans += std::min(neededTime[i - 1], neededTime[i]);
                neededTime[i] = std::max(neededTime[i - 1], neededTime[i]);
            }
        }
        return ans;
    }   
```