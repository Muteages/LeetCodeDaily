# Grumpy Bookstore Owner

https://leetcode.com/problems/grumpy-bookstore-owner

There is a bookstore owner that has a store open for n minutes. Every minute, some number of customers enter the store. You are given an integer array customers of length n where customers[i] is the number of the customer that enters the store at the start of the ith minute and all those customers leave after the end of that minute.

On some minutes, the bookstore owner is grumpy. You are given a binary array grumpy where grumpy[i] is 1 if the bookstore owner is grumpy during the ith minute, and is 0 otherwise.

When the bookstore owner is grumpy, the customers of that minute are not satisfied, otherwise, they are satisfied.

The bookstore owner knows a secret technique to keep themselves not grumpy for minutes consecutive minutes, but can only use it once.

Return the maximum number of customers that can be satisfied throughout the day.

## Approach 

``` JavaScript
var maxSatisfied = function(customers, grumpy, minutes) {
    let satisfied = 0, unsatisfied = 0;
    for (let i = 0; i < minutes; i++) {
        satisfied += (1 - grumpy[i]) * customers[i];
        unsatisfied += grumpy[i] * customers[i];
    }

    let extraSatisfied = unsatisfied;
    for (let i = minutes; i < customers.length; i++) {
        satisfied += (1 - grumpy[i]) * customers[i];
        unsatisfied += grumpy[i] * customers[i] - grumpy[i - minutes] * customers[i - minutes];
        extraSatisfied = Math.max(extraSatisfied, unsatisfied);
    }
    return satisfied + extraSatisfied;
};
```