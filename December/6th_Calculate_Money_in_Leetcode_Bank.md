# Calculate Money in Leetcode Bank

https://leetcode.com/problems/calculate-money-in-leetcode-bank

Hercy wants to save money for his first car. He puts money in the Leetcode bank every day.

He starts by putting in $1 on Monday, the first day. Every day from Tuesday to Sunday, he will put in $1 more than the day before. On every subsequent Monday, he will put in $1 more than the previous Monday.
Given n, return the total amount of money he will have in the Leetcode bank at the end of the nth day.

## Approach 1

Brute force
``` C++
    int totalMoney(int n) {
        int ans = 0;
        int week = 0;
        while (n > 0)
        {
            week++;
            int curr = n > 7 ? 7 : n; // Remaining days of current week
            for (int i = 0; i < curr; i++)
            {
                ans += week + i;
            }
            n -= 7;
        }
        return ans;
    }
```

## Approach 2

First week total : 28

``` C++
    int totalMoney(int n) {
        int week = n / 7;
        int rem = n % 7;
        int ans = 28 * week + 7 * week * (week - 1) / 2;
        if (rem != 0)
        {
            ans += (week + 1) * rem + (rem - 1) * rem / 2;     // Sn = n * a1 + (n - 1) * n * d / 2
            // ans += (week + 1 + week + 1 + rem - 1) * rem / 2;  // Sn = (a1 + an) * n / 2
        }
        return ans;
    }
```