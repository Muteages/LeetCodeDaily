# Height Checker

https://leetcode.com/problems/height-checker

A school is trying to take an annual photo of all the students. The students are asked to stand in a single file line in non-decreasing order by height. Let this ordering be represented by the integer array expected where expected[i] is the expected height of the ith student in line.

You are given an integer array heights representing the current order that the students are standing in. Each heights[i] is the height of the ith student in line (0-indexed).

Return the number of indices where heights[i] != expected[i].

## Approach 

``` JavaScript
var heightChecker = function(heights) {
    let freq = new Array(101).fill(0);
    for (let height of heights) {
        freq[height]++;
    }

    let ans = 0;
    let i = 0;
    for (let j = 0; j < 101; j++) {
        if (freq[j] === 0) {
            continue;
        }
        let f = freq[j];
        while (f--) {
            if (heights[i] != j) {
                ans++;
            }
            i++;
        }
    }
    return ans;
};
```

Built-in sorting 

``` JavaScript
var heightChecker = function(heights) {
    const sorted = heights.slice().sort((a, b) => a - b);
    let ans = 0;
    for (let i = 0; i < heights.length; i++) {
        if (heights[i] !== sorted[i]) {
            ans++;
        }
    }
    return ans;
};
```