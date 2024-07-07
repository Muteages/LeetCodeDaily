# Water Bottles
https://leetcode.com/problems/water-bottles

There are numBottles water bottles that are initially full of water. You can exchange numExchange empty water bottles from the market with one full water bottle.

The operation of drinking a full water bottle turns it into an empty bottle.

Given the two integers numBottles and numExchange, return the maximum number of water bottles you can drink.

## Approach 

``` C++
    int numWaterBottles(int numBottles, int numExchange) {
        int ans = numBottles;
        while (numBottles >= numExchange)
        {
            auto[reuse, empty] = std::div(numBottles, numExchange);
            ans += reuse;
            numBottles = empty + reuse;
        }
        return ans;
    }
```

``` C++
    int numWaterBottles(int numBottles, int numExchange) {
        int ans = numBottles, empty{};
        while (numBottles >= numExchange)
        {
            empty = numBottles / numExchange;
            ans += empty;
            empty += numBottles % numExchange;
            numBottles = empty;
        }
        return ans;
    }
```

``` C++
    int exchange(int curr, int ex)
    {
        if (curr < ex)
        {
            return 0;
        }
        auto [reuse, rem] = std::div(curr, ex);
        return reuse + exchange(reuse + rem, ex);
    }

    int numWaterBottles(int numBottles, int numExchange) {
        return numBottles + exchange(numBottles, numExchange);
    }
```