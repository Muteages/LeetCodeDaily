# Magnitic Force Between Two Balls

https://leetcode.com/problems/magnetic-force-between-two-balls

In the universe Earth C-137, Rick discovered a special form of magnetic force between two balls if they are put in his new invented basket. Rick has n empty baskets, the ith basket is at position[i], Morty has m balls and needs to distribute the balls into the baskets such that the minimum magnetic force between any two balls is maximum.

Rick stated that magnetic force between two different balls at positions x and y is |x - y|.

Given the integer array position and the integer m. Return the required force.

## Approach 

``` JavaScript
const isPossible = (position, force, m) => {
    let balls = 2, prev = 0, last = position.length - 1; // Since we can put two balls at head and tail, the initial number is 2.
    for (let i = 1; i < last; i++) {
        if (position[i] - position[prev] >= force && position[last] - position[i] >= force) {
            balls++;
            prev = i;
        }
        if (balls === m ) {
            return true;
        }
    }
    return false;
}

var maxDistance = function(position, m) {
    position.sort((a, b) => a - b);
    const n = position.length;
    let left = 1, right = Math.floor(position[n - 1] - position[0] / (m - 1)); // min force and max force
    if (m === 2) {
        return right;
    }
    let ans = 0;
    while (left <= right) {
        let mid = Math.floor(left + (right - left) / 2);
        if (isPossible(position, mid, m)) {
            left = mid + 1;
            ans = mid;
        }
        else {
            right = mid - 1;
        }
    }
    return ans;
};
```