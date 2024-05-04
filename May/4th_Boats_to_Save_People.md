# Boats to Save People

https://leetcode.com/problems/boats-to-save-people

You are given an array people where people[i] is the weight of the ith person, and an infinite number of boats where each boat can carry a maximum weight of limit. Each boat carries at most two people at the same time, provided the sum of the weight of those people is at most limit.

Return the minimum number of boats to carry every given person.

 

## Approach 
``` C++
    int numRescueBoats(vector<int>& people, int limit) {
        std::sort(people.begin(), people.end());
        int n = people.size();
        if (people[0] >= limit)
        {
            return n;
        }
        int left = 0, right = n - 1;
        int boats = 0;
        while (left <= right)
        {
            if (people[right] + people[left] <= limit)
            { // Enable to carry the current lighest person as well
                left++;
            }
            right--; // Always carry the current heaviest person
            boats++;
        }
        return boats;
    }
```