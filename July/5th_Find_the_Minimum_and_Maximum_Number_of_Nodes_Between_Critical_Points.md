# Find the Minimum and Maximum Number of Nodes Between Critical Points

https://leetcode.com/problems/find-the-minimum-and-maximum-number-of-nodes-between-critical-points

Given a linked list head, return an array of length 2 containing [minDistance, maxDistance] where minDistance is the minimum distance between any two distinct critical points and maxDistance is the maximum distance between any two distinct critical points. If there are fewer than two critical points, return [-1, -1].


## Approach 1

``` JavaScript
var nodesBetweenCriticalPoints = function(head) {
    const critical = [Number.NEGATIVE_INFINITY];
    let min = Number.POSITIVE_INFINITY;
    let prev = head, curr = head.next, next = head.next.next, idx = 1;
    while (next) {
        if ((curr.val > prev.val && curr.val > next.val) || (curr.val < prev.val && curr.val < next.val)) {
            const last = critical.at(-1);
            min = Math.min(min, idx - last);
            critical.push(idx);
        }
        prev = curr;
        curr = next;
        next = next.next;
        idx++;
    }

    const n = critical.length;
    if (n < 3) {
        return [-1, -1];
    }
    let max = critical[n - 1] - critical[1];
    return [min, max];
};
```

## Approach 2

Use variable instead of array

``` JavaScript
var nodesBetweenCriticalPoints = function(head) {
    let first = -1, last = -1, idx = 1, min = Infinity;
    let prev = head, curr = head.next, next = head.next.next;
    while (next) {
        if ((curr.val > prev.val && curr.val > next.val) || (curr.val < prev.val && curr.val < next.val)) {
            if (first === -1) {
                first = idx;
            }
            if (last !== -1) {
                min = Math.min(min, idx - last);
            }
            last = idx;
        }
        prev = curr;
        curr = next;
        next = next.next;
        idx++;
    }
    if (first === last) {
        return [-1, -1];
    }
    let max = last - first;
    return [min, max];
};
```

``` C++
    vector<int> nodesBetweenCriticalPoints(ListNode* head) {
        int first = -1, last = -1, idx = 1, minDist = INT_MAX;
        ListNode* prev = head, *curr = head->next, *next = head->next->next;
        while (next)
        {
            if ((curr->val > prev->val && curr->val > next->val) || (curr->val < prev->val && curr->val < next->val))
            {
                if (first == -1)
                {
                    first = idx;
                }
                if (last != -1)
                {
                    minDist = std::min(minDist, idx - last);
                }
                last = idx;
            }
            idx++;
            prev = curr;
            curr = next;
            next = next->next;
        }

        if (first == last)
        {
            return {-1, -1};
        }
        return {minDist, last - first};
    }
```