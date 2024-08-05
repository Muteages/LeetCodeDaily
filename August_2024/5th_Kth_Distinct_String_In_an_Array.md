# Kth Distinct String in an Array

A distinct string is a string that is present only once in an array.

Given an array of strings arr, and an integer k, return the kth distinct string present in arr. If there are fewer than k distinct strings, return an empty string "".

Note that the strings are considered in the order in which they appear in the array.


## Approach 

``` JavaScript
var kthDistinct = function(arr, k) {
    let freq = {};
    for (let s of arr){
        freq[s] = (freq[s] || 0) + 1;
    }

    for (let s of arr)
    {
        if (freq[s] === 1) k--;
        if (k === 0) return s; 
    }
    return "";
};
```

## Approach 2

``` JavaScript
var kthDistinct = function(arr, k) {
    let distincts = [];
    for (let s of arr) {
        if (arr.indexOf(s) === arr.lastIndexOf(s)) {
            distincts.push(s);
        }
    }
    return distincts.length >= k ? distincts[k - 1] : "";
};
```
