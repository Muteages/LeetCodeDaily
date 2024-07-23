# Sort Array by Increasing Frequency

Given an array of integers nums, sort the array in increasing order based on the frequency of the values. If multiple values have the same frequency, sort them in decreasing order.

Return the sorted array.

##  Approach

``` JavaScript
var frequencySort = function(nums) {
    const freq = Array(201).fill(0);
    for (let num of nums) {
        freq[num + 100]++;
    }
    nums.sort((a, b) => freq[a + 100] === freq[b + 100] ? b - a : freq[a + 100] - freq[b + 100]);
    return nums;
};
```