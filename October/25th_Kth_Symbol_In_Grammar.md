# Kth Symbol in Grammar

https://leetcode.com/problems/k-th-symbol-in-grammar

We build a table of n rows (1-indexed). We start by writing 0 in the 1st row. Now in every subsequent row, we look at the previous row and replace each occurrence of 0 with 01, and each occurrence of 1 with 10.

For example, for n = 3, the 1st row is 0, the 2nd row is 01, and the 3rd row is 0110.
Given two integer n and k, return the kth (1-indexed) symbol in the nth row of a table of n rows.

## Approach 

``` C++
    int kthGrammar(int n, int k) {
        // Basic pattern: 01
        if (n == 1 || k == 1)
        {
            return 0;
        }
        else if (k == 2)
        {
            return 1;
        }

        int flipCnt = 0;
        int total = std::pow(2, n - 1);
        while (total > 2)
        {
            total /= 2;
            if (k > total)
            { // Move the position and record the flip time
                k = k - total;
                flipCnt++;
            }
        }
        // Convert to the basic 01 pattern
        int ans = (k == 1) ? 0 : 1;
        if (flipCnt % 2 != 0)
        {
            ans ^= 1;
        }
        return ans;        
    }
```