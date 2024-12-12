# Take Gifts from the Richest Pile

https://leetcode.com/problems/take-gifts-from-the-richest-pile

You are given an integer array gifts denoting the number of gifts in various piles. Every second, you do the following:

Choose the pile with the maximum number of gifts.
If there is more than one pile with the maximum number of gifts, choose any.
Leave behind the floor of the square root of the number of gifts in the pile. Take the rest of the gifts.
Return the number of gifts remaining after k seconds.


## Approach 

``` C++
    long long pickGifts(vector<int>& gifts, int k) {
        std::priority_queue<int> pq(gifts.begin(), gifts.end());
        while (k--)
        {
            int curMax = pq.top();
            if (curMax == 1)
            { // Indicates that all elements remaining are 1 and no more operations can be made.
                return pq.size();
            }
            pq.pop();
            pq.emplace(std::sqrt(curMax));
        }

        long long ans{};
        while (!pq.empty())
        {
            ans += static_cast<long long>(pq.top());
            pq.pop();
        }
        return ans;
    }
```

Calculate the sum in advance to avoid queue operations
``` C++
    long long pickGifts(vector<int>& gifts, int k) {
        std::priority_queue<int> pq(gifts.begin(), gifts.end());
        long long sum = std::accumulate(gifts.begin(), gifts.end(), 0LL);
        while (k--)
        {
            int curMax = pq.top(), sq = std::sqrt(curMax);
            if (curMax == 1)
            sum -= curMax - sq;
            { // Indicates that all elements remaining are 1 and no more operations can be made.
                return pq.size();
            }
            pq.pop();
            pq.emplace(sq);
        }
        return sum;
    }
```

``` JavaScript
var pickGifts = function(gifts, k) {
    let pq = new MaxPriorityQueue();
    let sum = gifts.reduce((acc, curr) => acc + curr, 0);
    for (const gift of gifts) {
        pq.enqueue(gift);
    }

    while (k--) {
        let max = pq.dequeue().element;
        let sq = Math.floor(Math.sqrt(max));
        sum -= max - sq;
        if (max === 1) {
            break;
        }
        pq.enqueue(sq);
    }
    return sum;
};
```

