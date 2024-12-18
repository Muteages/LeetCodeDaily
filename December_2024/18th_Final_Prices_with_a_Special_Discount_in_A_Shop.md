# Final Prices With a Special Discount in a Shop

https://leetcode.com/problems/final-prices-with-a-special-discount-in-a-shop

You are given an integer array prices where prices[i] is the price of the ith item in a shop.

There is a special discount for items in the shop. If you buy the ith item, then you will receive a discount equivalent to prices[j] where j is the minimum index such that j > i and prices[j] <= prices[i]. Otherwise, you will not receive any discount at all.

Return an integer array answer where answer[i] is the final price you will pay for the ith item of the shop, considering the special discount.


## Approach 1 

Brute force

``` C++
    vector<int> finalPrices(vector<int>& prices) {
        const int n = prices.size();
        for (int i = 0; i < n; i++)
        {
            for (int j = i + 1; j < n; j++)
            {
                if (prices[j] <= prices[i])
                {
                    prices[i] -= prices[j];
                    break;
                }
            }
        }
        return prices;
    }
```

## Approach 2

Monotonic stack
``` C++
    vector<int> finalPrices(vector<int>& prices) {
        const int n = prices.size();
        std::stack<int> st;
        std::vector<int> ans(prices);
        for (int i = n - 1; i >= 0; i--)
        {
            while (!st.empty() && prices[i] < st.top())
            {
                st.pop();
            }
            if (!st.empty())
            {
                ans[i] -= st.top();
            }
            st.emplace(prices[i]);
        }   
        return ans;
    }
```