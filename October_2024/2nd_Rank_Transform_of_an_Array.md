# Rank Transform of an Array



## Approach 

``` C++
    vector<int> arrayRankTransform(vector<int>& arr) {
        if (arr.empty()) return {};
        int n = arr.size();
        std::vector<std::pair<int, int>> e2i(n); // element and corresponding index
        for (int i = 0; i < n; i++)
        {
            e2i[i] = {arr[i], i};
        }
        std::sort(e2i.begin(), e2i.end());
        arr[e2i[0].second] = 1;
        for (int i = 1; i < n; i++)
        {
            // If current element is equal to previous element, then they are allocated the same rank, otherwise get previous + 1
            arr[e2i[i].second] = arr[e2i[i - 1].second] + (e2i[i].first != e2i[i - 1].first);
        }
        return arr;
    }
```

``` JavaScript
var arrayRankTransform = function(arr) {
    const sorted = arr.map((ele, idx) => [ele, idx]).sort((a, b) => a[0] - b[0]);

    let prev = -Infinity, rank = 0;
    for (let [ele, idx] of sorted) {
        if (ele > prev) rank++;
        arr[idx] = rank;
        prev = ele;
    }
    return arr;
};
```