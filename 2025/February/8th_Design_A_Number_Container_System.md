# Design a Number Container System

https://leetcode.com/problems/design-a-number-container-system

Design a number container system that can do the following:

Insert or Replace a number at the given index in the system.
Return the smallest index for the given number in the system.
Implement the NumberContainers class:

NumberContainers() Initializes the number container system.
void change(int index, int number) Fills the container at index with the number. If there is already a number at that index, replace it.
int find(int number) Returns the smallest index for the given number, or -1 if there is no index that is filled by number in the system.

## Approach 

``` C++
class NumberContainers {
public:
    NumberContainers() {
        
    }
    
    void change(int index, int number) {
        ump[index] = number;
        idx[number].emplace(index);
    }
    
    int find(int number) {
        if (!idx.count(number)) return -1;
        while (!idx[number].empty())
        {
            int curIdx = idx[number].top();
            if (ump[curIdx] == number) return curIdx;
            idx[number].pop(); // Indicates current number has been replaced, thus pop it
        }
        return -1;
    }
private:
    std::unordered_map<int, int> ump; // idx - number
    std::unordered_map<int, std::priority_queue<int, std::vector<int>, std::greater<int>>> idx; // number - ordered indices
};
```

``` Python
class NumberContainers:

    def __init__(self):
        self.mp = {}
        self.idx = defaultdict(list)

    def change(self, index: int, number: int) -> None:
        self.mp[index] = number
        heapq.heappush(self.idx[number], index)

    def find(self, number: int) -> int:
        if number not in self.idx:
            return -1
        while self.idx[number]:
            cur_idx = self.idx[number][0]
            if self.mp[cur_idx] == number:
                return cur_idx
            heapq.heappop(self.idx[number])
        return -1
```

``` JavaScript
var NumberContainers = function() {
    this.mp = new Map();
    this.idx = new Map();
};

/** 
 * @param {number} index 
 * @param {number} number
 * @return {void}
 */
NumberContainers.prototype.change = function(index, number) {
    this.mp.set(index, number);
    if (!this.idx.has(number)) {
        this.idx.set(number, new MinPriorityQueue());
    }
    this.idx.get(number).enqueue(index);
};

/** 
 * @param {number} number
 * @return {number}
 */
NumberContainers.prototype.find = function(number) {
        if (!this.idx.has(number)) {
            return -1;
        }
        while (this.idx.get(number).size() > 0) {
            let curIdx = this.idx.get(number).front().element;
            if (this.mp.get(curIdx) === number) {
                return curIdx;
            }
            this.idx.get(number).dequeue();
        }
        return -1;
};
```