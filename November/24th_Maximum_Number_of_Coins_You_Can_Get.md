# Maximum Number of Coins You Can Get

https://leetcode.com/problems/maximum-number-of-coins-you-can-get

There are 3n piles of coins of varying size, you and your friends will take piles of coins as follows:

In each step, you will choose any 3 piles of coins (not necessarily consecutive).
Of your choice, Alice will pick the pile with the maximum number of coins.
You will pick the next pile with the maximum number of coins.
Your friend Bob will pick the last pile.
Repeat until there are no more piles of coins.
Given an array of integers piles where piles[i] is the number of coins in the ith pile.

Return the maximum number of coins that you can have.

## Approach 1
Straight forward sorting

``` C++
    int maxCoins(vector<int>& piles) {
       std::sort(piles.begin(), piles.end());
       int n = piles.size();
       int ans = 0;
       for (int i = n / 3; i < n; i += 2)
       {
           ans += piles[i];
       }
       return ans;
    }
```

## Approach 2

Frequency count
``` C++
    int maxCoins(vector<int>& piles) {
        int maxCoin = -1;
        for (int& pile : piles)
        {
            maxCoin = std::max(maxCoin, pile);
        }
        std::vector<int> freq(maxCoin + 1, 0);
        for (int& pile : piles)
        {
            freq[pile]++;
        }

        int ans = 0;
        bool isCount = false;
        int n = piles.size() / 3;
        int curr = maxCoin;
        while (n > 0)
        {
            if (freq[curr] > 0)
            {
                freq[curr]--;
                if (isCount)
                { // Pick the current pile
                    ans += curr;
                    n--;
                    isCount = false;
                }
                else
                { // Alice's pile, skip
                    isCount = true;
                }
            }
            else
            {
                curr--;
            }
        }
        return ans;
    }
```
