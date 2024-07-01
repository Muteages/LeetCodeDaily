# Three Consecutive Odds

https://leetcode.com/problems/three-consecutive-odds

Given an integer array arr, return true if there are three consecutive odd numbers in the array. Otherwise, return false.
 


## Approach 

``` JavaScript
var threeConsecutiveOdds = function(arr) {
    let cnt = 0;
    for (let ele of arr) {
        if (ele & 1) {
            cnt++;
        }
        else {
            cnt = 0;
        }
        if (cnt === 3) {
            return true;
        }
    }
    return false;
};
```