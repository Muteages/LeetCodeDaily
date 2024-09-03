# Sum of Digits of String after Convert

https://leetcode.com/problems/sum-of-digits-of-string-after-convert


You are given a string s consisting of lowercase English letters, and an integer k.

First, convert s into an integer by replacing each letter with its position in the alphabet (i.e., replace 'a' with 1, 'b' with 2, ..., 'z' with 26). Then, transform the integer by replacing it with the sum of its digits. Repeat the transform operation k times in total.

## Approach 

``` JavaScript
var getLucky = function(s, k) {
    let sum = 0;
    for (let ch of s) {
        let num = ch.charCodeAt(0) - 'a'.charCodeAt(0) + 1;
        sum += Math.floor(num / 10) + (num % 10);
    }

    while (--k) {
        let temp = 0;
        while (sum > 0) {
            temp += sum % 10;
            sum = Math.floor(sum / 10);
        }
        sum = temp;
    }
    return sum;
};
```