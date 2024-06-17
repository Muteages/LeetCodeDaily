# Sum of Square Numbers

https://leetcode.com/problems/sum-of-square-numbers


Given a non-negative integer c, decide whether there're two integers a and b such that a2 + b2 = c.

## Approach 

``` JavaScript
var judgeSquareSum = function(c) {
    let left = 0, right = Math.floor(Math.sqrt(c));
    while (left <= right) {
        let mid = Math.floor(left + (right - left) / 2);
        let sum = left ** 2 + right ** 2;
        if (sum === c) {
            return true;
        }
        else if (sum < c) {
            left = c > (mid ** 2 + right ** 2) ? mid + 1 : left + 1;
        }
        else {
            right = c < (left ** 2 + mid ** 2) ? mid - 1 : right - 1;
        }
    }
    return false;
};
```