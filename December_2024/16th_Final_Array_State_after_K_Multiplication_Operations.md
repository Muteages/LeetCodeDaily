# Final Array State after K Multiplication Operations

https://leetcode.com/problems/final-array-state-after-k-multiplication-operations-i

You are given an integer array nums, an integer k, and an integer multiplier.

You need to perform k operations on nums. In each operation:

Find the minimum value x in nums. If there are multiple occurrences of the minimum value, select the one that appears first.
Replace the selected minimum value x with x * multiplier.
Return an integer array denoting the final state of nums after performing all k operations.


## Approach 

``` C++
    using int2 = std::pair<int, int>;
    vector<int> getFinalState(vector<int>& nums, int k, int multiplier) {
        std::priority_queue<int2, std::vector<int2>, std::greater<int2>> pq;
        for (int i = 0; i < nums.size(); i++)
        {
            pq.emplace(nums[i], i);
        }

        while (k--)
        {
            auto [num, pos] = pq.top();
            pq.pop();
            num *= multiplier;
            nums[pos] = num;
            pq.emplace(num, pos);
        }
        return nums;
    }
```


``` JavaScript 1
var getFinalState = function(nums, k, multiplier) {
    while (k--) {
        let pos = nums.indexOf(Math.min(...nums));
        nums[pos] *= multiplier;
    }
    return nums;
};
```

``` JavaScript 2
var getFinalState = function(nums, k, multiplier) {
    const pq = new MinPriorityQueue();
    nums.forEach((num, idx) => {
        pq.enqueue(num * 1000 + idx);
    });

    while (k--) {
        let combined = pq.dequeue().element;
        let num = Math.floor(combined / 1000), pos = combined % 1000;
        num *= multiplier;
        nums[pos] = num;
        pq.enqueue(num * 1000 + pos);
    }
    return nums;
};
```