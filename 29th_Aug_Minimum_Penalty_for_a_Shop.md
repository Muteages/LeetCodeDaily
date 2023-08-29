# Minimum Penalty for a Shop

https://leetcode.com/problems/minimum-penalty-for-a-shop/description/

You are given the customer visit log of a shop represented by a 0-indexed string customers consisting only of characters 'N' and 'Y':

if the ith character is 'Y', it means that customers come at the ith hour
whereas 'N' indicates that no customers come at the ith hour.
If the shop closes at the jth hour (0 <= j <= n), the penalty is calculated as follows:

For every hour when the shop is open and no customers come, the penalty increases by 1.
For every hour when the shop is closed and customers come, the penalty increases by 1.
Return the earliest hour at which the shop must be closed to incur a minimum penalty.

Note that if a shop closes at the jth hour, it means the shop is closed at the hour j.


## Approach 1

Brute force: TLE

``` C++
    int bestClosingTime(string customers) {
        customers += 'T'; // Hence we need to consider the last character, adding a extra character here.
        int ans = 0;
        int penalty = INT_MAX;
        for (int close = 0; close < customers.size(); close++)
        { // Loop all possible close time
            int tempPenalty = 0;
            for (int i = 0; i < customers.size(); i++)
            {
                if (i < close && customers[i] == 'N')
                {
                    tempPenalty += 1;
                }
                else if (i >= close && customers[i] == 'Y')
                {
                    tempPenalty += 1;
                }
            }

            if (tempPenalty < penalty)
            { // Update penalty and time records
                penalty = tempPenalty;
                ans = close;
            }
        }
        return ans;
    }
```

## Approach 2 

A single loop to calculate the minimum penalty.

``` C++
    int bestClosingTime(string customers) {
        int closingTime = -1;
        int minPenalty = 0;
        int curPenalty = 0;
        for (int i = 0; i < customers.length(); i++)
        {
            curPenalty += (customers[i] == 'N') ? 1 : -1;
            if (curPenalty < minPenalty)
            {
                closingTime = i;
                minPenalty = curPenalty;
            }
        }
        return closingTime + 1;
    }
```