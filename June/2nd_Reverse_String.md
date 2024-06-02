# Reverse String

Write a function that reverses a string. The input string is given as an array of characters s.

You must do this by modifying the input array in-place with O(1) extra memory.


## Approach 

``` JavaScript
var reverseString = function(s) {
    let l = 0, r = s.length - 1;
    while (l <= r)
    {
        [s[l], s[r]] = [s[r], s[l]];
        l++;
        r--;
    }
```