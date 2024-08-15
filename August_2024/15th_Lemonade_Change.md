# Lemonade Change

https://leetcode.com/problems/lemonade-change

At a lemonade stand, each lemonade costs $5. Customers are standing in a queue to buy from you and order one at a time (in the order specified by bills). Each customer will only buy one lemonade and pay with either a $5, $10, or $20 bill. You must provide the correct change to each customer so that the net transaction is that the customer pays $5.

Note that you do not have any change in hand at first.

Given an integer array bills where bills[i] is the bill the ith customer pays, return true if you can provide every customer with the correct change, or false otherwise.


## Approach 

``` C++
    bool lemonadeChange(vector<int>& bills) {
        int cnt5 = 0, cnt10 = 0;
        for (int bill : bills)
        {
            if (bill == 5)
            {
                cnt5++;
                continue;
            }
            else if (bill == 10)
            {
                if (cnt5 > 0)
                {
                    cnt5--;
                    cnt10++;
                }
                else
                {
                    return false;
                }
            }
            else
            { // bill == 20
                if (cnt10 > 0 && cnt5 > 0)
                {
                    cnt10--;
                    cnt5--;
                }
                else if (cnt5 >= 3)
                {
                    cnt5 -= 3;
                }
                else 
                {
                    return false;
                }
            }
        }
        return true;
    }
```