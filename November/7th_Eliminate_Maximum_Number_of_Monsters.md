# Eliminate Maximum Number of Monsters

https://leetcode.com/problems/eliminate-maximum-number-of-monsters

You are playing a video game where you are defending your city from a group of n monsters. You are given a 0-indexed integer array dist of size n, where dist[i] is the initial distance in kilometers of the ith monster from the city.

The monsters walk toward the city at a constant speed. The speed of each monster is given to you in an integer array speed of size n, where speed[i] is the speed of the ith monster in kilometers per minute.

You have a weapon that, once fully charged, can eliminate a single monster. However, the weapon takes one minute to charge. The weapon is fully charged at the very start.

You lose when any monster reaches your city. If a monster reaches the city at the exact moment the weapon is fully charged, it counts as a loss, and the game ends before you can use your weapon.

Return the maximum number of monsters that you can eliminate before you lose, or n if you can eliminate all the monsters before they reach the city.


## Approach 

``` C++
    int eliminateMaximum(vector<int>& dist, vector<int>& speed) {
        int n = dist.size();
        std::vector<double> arriveTime(n);

        for (int i = 0; i < n; i++)
        {
            arriveTime[i] = dist[i] / (double)speed[i];
        }

        std::sort(arriveTime.begin(), arriveTime.end());

        int ans = 1; // We can eliminate at least one monster at time 0
        for (int i = 1; i < n; i++)
        {
            if (arriveTime[i] > i)
            { // No monster reaches the city
                ans++;
            }
            else
            {
               break;
            }
        }
        return ans;
    }
```

## Approach 2

Prefix 
``` C++
    int eliminateMaximum(vector<int>& dist, vector<int>& speed) {
        int n = dist.size();

        for (int i = 0; i < n; i++)
        { // Initialise dist and speed to arrivalTime and monsterCount at each time
            dist[i] = std::ceil(dist[i] / (double)speed[i]); 
            speed[i] = 0; 
        }

        for (auto& time : dist)
        {
            if(time < n)
            {
                speed[time]++;
            }
        }
        
        for (int i = 1; i < n; i++)
        {
            speed[i] += speed[i - 1]; // total monsters at current time

            if (speed[i] > i)
            { // Unable to eliminate all, indicates fail the mission
                return i;
            }
        }
        return n;
    }
```