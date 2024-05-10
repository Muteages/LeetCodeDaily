# K-th Smallest Prime Fraction

https://leetcode.com/problems/k-th-smallest-prime-fraction

You are given a sorted integer array arr containing 1 and prime numbers, where all the integers of arr are unique. You are also given an integer k.

For every i and j where 0 <= i < j < arr.length, we consider the fraction arr[i] / arr[j].

Return the kth smallest fraction considered. Return your answer as an array of integers of size 2, where answer[0] == arr[i] and answer[1] == arr[j].


## Approach 1

``` C++
    vector<int> kthSmallestPrimeFraction(vector<int>& arr, int k) {
        int n = arr.size();
        std::priority_queue<std::tuple<float, int, int>, std::vector<std::tuple<float, int, int>>, std::greater<>> pq;
        for (int i = n - 1; i >= 0; i--)
        {
            for (int j = 0; j < i; j++)
            {
                pq.emplace((float)arr[j] / arr[i], arr[j], arr[i]);
            }
        }
        while (k > 1)
        {
            pq.pop();
            k--;
        }
        auto [f, i, j] = pq.top();
        return {i, j};
    }
```

## Approach 2

Optimal solution

``` C++
    vector<int> kthSmallestPrimeFraction(vector<int>& arr, int k) {
        std::priority_queue<std::tuple<float, int, int>, std::vector<std::tuple<float, int, int>>, std::greater<>> pq;
        int n = arr.size();
        for (int i = 0; i < n; i++)
        {
            pq.emplace(float(arr[i]) / arr[n - 1], i, n - 1);
        }

        // The next smallest fraction is always the next with the same denominator or with the same numerator and denominator - 1
        while (k-- > 1)
        {
            auto [f, num, den] = pq.top();
            pq.pop();
            pq.emplace(float(arr[num]) / arr[den - 1], num, den - 1);
        }
        
        auto [f, num, den] = pq.top();
        return {arr[num], arr[den]};
    }
```

With custom comparator

``` C++
    vector<int> kthSmallestPrimeFraction(vector<int>& arr, int k) {
        int n = arr.size();
        auto comp = [&](std::pair<int, int> f1, std::pair<int, int>f2){
            return arr[f1.first] * arr[f2.second] > arr[f1.second] * arr[f2.first];
        };

        std::priority_queue<std::pair<int, int>, std::vector<std::pair<int, int>>, decltype(comp)> pq(comp);
        for (int i = n - 2; i >= 0; i--)
        {
            pq.emplace(i, n - 1);
        }

        while (k-- > 1)
        {
            auto [num, den] = pq.top();
            pq.pop();
            pq.emplace(num, den - 1);
        }

        auto [num, den] = pq.top();
        return {arr[num], arr[den]};
    }
```