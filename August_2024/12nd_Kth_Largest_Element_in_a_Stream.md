# Kth Largest Element in a Stream

https://leetcode.com/problems/kth-largest-element-in-a-stream

Design a class to find the kth largest element in a stream. Note that it is the kth largest element in the sorted order, not the kth distinct element.

Implement KthLargest class:

KthLargest(int k, int[] nums) Initializes the object with the integer k and the stream of integers nums.
int add(int val) Appends the integer val to the stream and returns the element representing the kth largest element in the stream.

## Approach 

``` C++
class KthLargest {
public:
    KthLargest(int k, vector<int>& nums) {
        this->k = k;
        for (int num : nums)
        {
            add(num);
        }
    }
    
    int add(int val) {
        if (pq.size() < k)
        {
            pq.emplace(val);
        }
        else if (pq.top() < val)
        {
            pq.pop();
            pq.emplace(val);
        }
        return pq.top();
    }
private:
    std::priority_queue<int, std::vector<int>, std::greater<int>> pq;
    int k;
};
```


Use external lib for priority queue.

``` JavaScript
var KthLargest = function(k, nums) {
    this.k = k;
    this.pq = new MinPriorityQueue();
    for (let num of nums) {
        this.add(num);
    }
};

KthLargest.prototype.add = function(val) {
    if (this.pq.size() < this.k) {
        this.pq.enqueue(val);
    }
    else if (this.pq.front().element < val) {
        this.pq.dequeue();
        this.pq.enqueue(val);
    }
    return this.pq.front().element;
};
```

Write a custom priority queue class manually.

``` JavaScript

```