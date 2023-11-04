# Last Moment Before All Ants Fall Out of a Plank

https://leetcode.com/problems/last-moment-before-all-ants-fall-out-of-a-plank

We have a wooden plank of the length n units. Some ants are walking on the plank, each ant moves with a speed of 1 unit per second. Some of the ants move to the left, the other move to the right.

When two ants moving in two different directions meet at some point, they change their directions and continue moving again. Assume changing directions does not take any additional time.

When an ant reaches one end of the plank at a time t, it falls out of the plank immediately.

Given an integer n and two integer arrays left and right, the positions of the ants moving to the left and the right, return the moment when the last ant(s) fall out of the plank.

## Approach 1

``` C++
    int getLastMoment(int n, vector<int>& left, vector<int>& right) {
        int time = INT_MIN;

        for (auto& ant : left)
        {
            time = std::max(time, ant);
        }

        if (time == n)
        { // Reach the max
            return time;
        }

        for (auto& ant : right)
        {
            time = std::max(time, n - ant);
        }
        return time;
    }
```

## Approach 2
``` C++
   int getLastMoment(int n, vector<int>& left, vector<int>& right) {
        std::sort(left.begin(), left.end());
        std::sort(right.begin(), right.end());

        if (left.empty() && right.empty())
        {
            return 0;
        }
        else if (left.empty())
        {
            return n - right.front();
        }
        else if (right.empty())
        {
            return left.back();
        }
        else
        {
            return std::max(left.back(), n - right.front());
        }
        return -1;
    }
```

## Approach 3
``` C++
    int getLastMoment(int n, std::vector<int>& left, std::vector<int>& right) {
        int l = left.empty() ? 0 : *max_element(left.begin(), left.end());
        int r = right.empty() ? n : *min_element(right.begin(), right.end());
        return max(l, n - r);
    }
```
