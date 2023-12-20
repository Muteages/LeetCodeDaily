# Buy two chocolates

https://leetcode.com/problems/buy-two-chocolates

You are given an integer array prices representing the prices of various chocolates in a store. You are also given a single integer money, which represents your initial amount of money.

You must buy exactly two chocolates in such a way that you still have some non-negative leftover money. You would like to minimize the sum of the prices of the two chocolates you buy.

Return the amount of money you will have leftover after buying the two chocolates. If there is no way for you to buy two chocolates without ending up in debt, return money. Note that the leftover must be non-negative.

## Approach 1

Sort and find two smallest number
``` C++
    int buyChoco(vector<int>& prices, int money) {
        std::sort(prices.begin(), prices.end());
        if (prices[0] + prices[1] > money)
        {
            return money;
        }
        return money - prices[0] - prices[1];
    }
```

## Approach 2

``` C++
    int buyChoco(vector<int>& prices, int money) {
        auto it = std::min_element(prices.begin(), prices.end());
        int smallest = *it;
        if (smallest >= money)
        {
            return money;
        }
        prices.erase(it);
        it = std::min_element(prices.begin(), prices.end());
        if (smallest + *it > money)
        {
            return money;
        }
        else
        {
            return money - smallest - *it;
        }
    }
```