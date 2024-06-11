# Relative Sort Array

https://leetcode.com/problems/relative-sort-array

## Approach 1

``` JavaScript
var relativeSortArray = function(arr1, arr2) {
    let freq = new Array(1001).fill(0);
    let maxNum = 0;
    arr1.forEach(num => {
        freq[num]++;
        maxNum = Math.max(maxNum, num);
    });

    let i = 0;
    arr2.forEach(num => {
        while (freq[num]-- > 0) { // Reorder the elements existing in arr2
            arr1[i++] = num;
        }
    });

    for (let j = 0; j <= maxNum; j++) { // Fill remaining elements
        while (freq[j]-- > 0) {
            arr1[i++] = j;
        }
    }
    return arr1;
};
```

## Appraoch 2

``` C++
    vector<int> relativeSortArray(vector<int>& arr1, vector<int>& arr2) {
        const int n1 = arr1.size(), n2 = arr2.size();
        std::vector<int> indices(1001, n2);

        for (int i = 0; i < n2; ++i)
        {
            indices[arr2[i]] = i;
        }

        std::sort(arr1.begin(), arr1.end(), [&](int a, int b) {
            if (indices[a] == indices[b])
            {
                return a < b;
            }
            return indices[a] < indices[b];
        });

        return arr1;
    }
```


``` JavaScript
var relativeSortArray = function(arr1, arr2) {
    const l1 = arr1.length, l2 = arr2.length;
    let indices = new Array(1001).fill(l2);
    for (let i = 0; i < l2; i++) {
        indices[arr2[i]] = i;
    }

    arr1.sort((a, b) => {
        if (indices[a] === indices[b]) {
            return a - b;
        }
        return indices[a] - indices[b];
    });
    return arr1;
};
```

