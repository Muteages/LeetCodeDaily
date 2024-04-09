# Time Needed to Buy Tickets

https://leetcode.com/problems/time-needed-to-buy-tickets

There are n people in a line queuing to buy tickets, where the 0th person is at the front of the line and the (n - 1)th person is at the back of the line.

You are given a 0-indexed integer array tickets of length n where the number of tickets that the ith person would like to buy is tickets[i].

Each person takes exactly 1 second to buy a ticket. A person can only buy 1 ticket at a time and has to go back to the end of the line (which happens instantaneously) in order to buy more tickets. If a person does not have any tickets left to buy, the person will leave the line.

Return the time taken for the person at position k (0-indexed) to finish buying tickets.


## Approach 1

Brute force

``` C++
    int timeRequiredToBuy(vector<int>& tickets, int k) {
        int time = 0;
        while (tickets[k] != 0)
        {
            for (int i = 0; i < tickets.size(); i++)
            {
                if (tickets[i] > 0)
                { // Check if there are any tickets left to buy
                    time++;
                    tickets[i]--;
                }
                if (i == k && tickets[i] == 0)
                {
                    break;
                }
            }
        }
        return time;
    }
```

## Approach 2

Sloved in one pass

``` C++
    int timeRequiredToBuy(vector<int>& tickets, int k) {
        int time = 0;
        int maxBuyable= tickets[k];
        for (int i = 0; i < tickets.size(); i++)
        {
            int buyable = (i <= k) ? maxBuyable : maxBuyable - 1;
            time += std::min(tickets[i], buyable);
        }
        return time;
    }
```