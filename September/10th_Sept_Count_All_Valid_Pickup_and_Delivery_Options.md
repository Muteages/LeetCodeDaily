# Count All Valid Pickup and Delivery Options

https://leetcode.com/problems/count-all-valid-pickup-and-delivery-options/description

Given n orders, each order consist in pickup and delivery services. 

Count all valid pickup/delivery possible sequences such that delivery(i) is always after of pickup(i). 

Since the answer may be too large, return it modulo 10^9 + 7.



## Approach

``` C++
    int mod = 1e9 + 7; 
    int countOrders(int n) {
        int64_t num = 1;
        for (int64_t i = 0; i < n; i++)
        {
            num = (num * (i + 1) * (2 * i + 1) % mod);
        }
        return num;
    }
```