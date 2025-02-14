# Minimum Operations to Exceed Threshold Value II

https://leetcode.com/problems/minimum-operations-to-exceed-threshold-value-ii

You are given a 0-indexed integer array nums, and an integer k.

You are allowed to perform some operations on nums, where in a single operation, you can:

Select the two smallest integers x and y from nums.
Remove x and y from nums.
Insert (min(x, y) * 2 + max(x, y)) at any position in the array.
Note that you can only apply the described operation if nums contains at least two elements.

Return the minimum number of operations needed so that all elements of the array are greater than or equal to k.

## Approach 

``` C++
    int minOperations(vector<int>& nums, int k) {
        std::priority_queue<int, std::vector<int>, std::greater<>> pq(nums.begin(), nums.end());
        int ans = 0;
        while (pq.size() >= 2 && pq.top() < k)
        {
            ans++;
            int a = pq.top();
            pq.pop();
            int b = pq.top();
            pq.pop();
            long long temp = 2LL * a + b;
            if (temp < k)
            {
                pq.emplace(temp);
            }
        }
        // Since we need to check int overflow and we might miss the last operation, check if there is a smaller number
        return (!pq.empty() && (pq.top() < k)) ? ans + 1 : ans;
    }
```

``` Python
    def minOperations(self, nums: List[int], k: int) -> int:
        heapq.heapify(nums)
        ans = 0
        while len(nums) >= 2 and nums[0] < k:
            ans += 1
            a = heapq.heappop(nums)
            b = heapq.heappop(nums)
            heapq.heappush(nums, 2 * a + b)
        
        return ans
```

``` JavaScript
// With PriorityQueue
var minOperations = function(nums, k) {
    let ans = 0;
    const pq = new PriorityQueue({compare: (a, b) => a - b});

    nums.forEach(num => pq.enqueue(num));

    while(pq._heap._nodes[0] < k && pq._heap._nodes.length >= 2){
        let x = pq.dequeue();
        let y = pq.dequeue();
        pq.enqueue(2 * x + y);
        ans++
    }
    return ans;
};

// With MinPriorityQueue
var minOperations = function(nums, k) {
    const pq = new MinPriorityQueue();
    for (let num of nums) {
        pq.enqueue(num);
    }

    let ans = 0;
    while (pq.front().element < k) {
        ans++;
        const x = pq.dequeue().element, y = pq.dequeue().element;
        const temp = 2 * x + y;
        pq.enqueue(temp);
    }
    return ans;
};
```