# Lexicographical Numbers

https://leetcode.com/problems/lexicographical-numbers

Given an integer n, return all the numbers in the range [1, n] sorted in lexicographical order.

You must write an algorithm that runs in O(n) time and uses O(1) extra space. 

## Approach 1

Iterative approach 

``` C++
    vector<int> lexicalOrder(int n) {
        std::vector<int> ans;
        ans.reserve(n);
        int num = 1;
        for (int i = 0; i < n; i++)
        {
            ans.emplace_back(num);
            if (num * 10 <= n)
            { // Indicates that there are high order numbers
                num *= 10;
            }
            else
            { // num * 10 > n.  Reach the highest digits, try to increament the lowest digit's number or decreament digits
                if (num == n)
                {
                    num /= 10;
                }
                num++;
                while (num % 10 == 0)
                { // Indicates the current lowest digits 1~9 are filled, decreament the digit to 1.
                    num /= 10;
                }
            }
        }
        return ans;
    }
```

## Approach 2

Recursive approach 

``` C++
    void recur(std::vector<int>& ans, int n, int curr)
    {
        if (curr > n) return;
        
        ans.emplace_back(curr);
        for (int i = 0; i <= 9; i++)
        {
            int next = curr * 10 + i;
            if (next > n) break;
            recur(ans, n, next);
        }

    }
    vector<int> lexicalOrder(int n) {
        std::vector<int> ans{};
        ans.reserve(n);
        for (int i = 1; i <= 9; i++)
        {
            recur(ans, n, i);
        }
        return ans;
    }
```

``` JavaScript
var lexicalOrder = function(n) {
    const ans = [];
    
    const recur = (st, end) => {
        while (st <= Math.min(end, n)) {
            ans.push(st);
            recur(st * 10, st * 10 + 9);
            st++;
        }
    };

    recur(1, 9);
    return ans;
};
```

