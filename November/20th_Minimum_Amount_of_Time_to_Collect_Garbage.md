# Minimum Amount of Time to Collect Garbage

https://leetcode.com/problems/minimum-amount-of-time-to-collect-garbage

You are given a 0-indexed array of strings garbage where garbage[i] represents the assortment of garbage at the ith house. garbage[i] consists only of the characters 'M', 'P' and 'G' representing one unit of metal, paper and glass garbage respectively. Picking up one unit of any type of garbage takes 1 minute.

You are also given a 0-indexed integer array travel where travel[i] is the number of minutes needed to go from house i to house i + 1.

There are three garbage trucks in the city, each responsible for picking up one type of garbage. Each garbage truck starts at house 0 and must visit each house in order; however, they do not need to visit every house.

Only one garbage truck may be used at any given moment. While one truck is driving or picking up garbage, the other two trucks cannot do anything.

Return the minimum number of minutes needed to pick up all the garbage.

## Approach 

``` C++
    int garbageCollection(vector<string>& garbage, vector<int>& travel) {
        int lastM = -1, lastP = -1, lastG = -1;
        int ans = 0;
        for (int i = 0; i < garbage.size(); i++)
        {
            for (const char& ch : garbage[i])
            { // Store the last occurrence house of each type of garbage
                if (ch == 'M')
                {
                    lastM = i;
                }
                else if (ch == 'P')
                {
                    lastP = i;
                }
                else
                {
                    lastG = i;
                }
                ans++;
            }
            if (i > 0 && i < garbage.size() - 1)
            { // Update the total needed travel time to each house
                travel[i] += travel[i - 1];
            }
        }

        if (lastM > 0)
        {
            ans += travel[lastM - 1];
        }
        if (lastP > 0)
        {
            ans += travel[lastP - 1];
        }
        if (lastG > 0)
        {
            ans += travel[lastG - 1];
        }
        return ans;
    }
```


## Approach 2
``` C++
    int garbageCollection(vector<string>& garbage, vector<int>& travel) {
        int ans = 0;
        int n = garbage.size();
        for (int i = 0; i < n; i++)
        {
            ans += garbage[i].length();
            if (i > 0 && i < n - 1)
            { // Update the total travel time to current house
                travel[i] += travel[i - 1];
            }
        }

        bool lastM = false, lastP = false, lastG = false;
        for (int i = garbage.size() - 1; i > 0; i--)
        {
            if (!lastM && garbage[i].find('M') != std::string::npos)
            {
                lastM = true;
                ans += i > 0 ? travel[i - 1] : 0;
            }
            if (!lastP && garbage[i].find('P') != std::string::npos)
            {
                lastP = true;
                ans += i > 0 ? travel[i - 1] : 0;
            }
            if (!lastG && garbage[i].find('G') != std::string::npos)
            {
                lastG = true;
                ans += i > 0 ? travel[i - 1] : 0;
            }
            if (lastM && lastP && lastG)
            {
                break;
            }
        }
        return ans;
    }
```