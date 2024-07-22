# Sort the People

https://leetcode.com/problems/sort-the-people


You are given an array of strings names, and an array heights that consists of distinct positive integers. Both arrays are of length n.

For each index i, names[i] and heights[i] denote the name and height of the ith person.

Return names sorted in descending order by the people's heights.

## Approach 

``` C++
    vector<string> sortPeople(vector<string>& names, vector<int>& heights) {
        std::priority_queue<std::pair<int, std::string>> pq;
        for (int i = 0; i < names.size(); i++)
        {
            pq.emplace(heights[i], names[i]);
        }
        int idx = 0;
        while (!pq.empty())
        {
            names[idx++] = pq.top().second;
            pq.pop();
        }
        return names;
    }
```

``` JavaScript
var sortPeople = function(names, heights) {
    let arr = [];
    for (let i = 0; i < names.length; i++) {
        arr.push([names[i], heights[i]]);
    }
    return arr.sort((a, b) => b[1] - a[1]).map(arr => arr[0]);
};
```

# Basic sorting excercise

## Approach 1

Bubble sort

``` JavaScript
var sortPeople = function(names, heights) {
    const len = heights.length;
    for (let i = 0; i < len; i++) {
        let sorted = true;
        for (let j = len - 1; j > i; j--) {
            if (heights[j] > heights[j - 1]) {
                [heights[j - 1], heights[j]] = [heights[j], heights[j - 1]];
                [names[j - 1], names[j]] = [names[j], names[j - 1]];
                sorted = false;
            }
        }
        if (sorted) break;
    }
    return names;
};
```

## Approach 2

Selection sort

``` JavaScript
var sortPeople = function(names, heights) {
    const len = heights.length;
    for (let i = 0; i < len; i++) {
        let max = i;
        for (let j = i + 1; j < len; j++) {
            max = heights[j] > heights[max] ? j : max;
        }
        [heights[i], heights[max]] = [heights[max], heights[i]];
        [names[i], names[max]] = [names[max], names[i]];
    }
    return names;
};
```

## Approach 3

Insertion sort

``` JavaScript
var sortPeople = function(names, heights) {
    const len = heights.length;
    for (let i = 1; i < len; i++) {
        let base = heights[i], name = names[i], j = i - 1;
        while (j >= 0 && heights[j] < base) {
            heights[j + 1] = heights[j];
            names[j + 1] = names[j];
            j--;
        }
        heights[j + 1] = base;
        names[j + 1] = name;
    }
    return names;
};
```

## Approach 4

Quick sort

``` JavaScript
var sortPeople = function(names, heights) {
    const quickSort = (left, right) => {
        if (left >= right) {
            return;
        }
        let pivot = partition(left, right);
        quickSort(left, pivot - 1);
        quickSort(pivot + 1, right);
    };

    const partition = (left, right) => {
        let i = left, j = right, base = heights[left];
        while (i < j) {
            while (i < j && heights[j] <= base) {
                j--;
            }
            while (i < j && heights[i] >= base) {
                i++;
            }
            [heights[i], heights[j], names[i], names[j]] = [heights[j], heights[i], names[j], names[i]];
        }
        [heights[i], heights[left], names[i], names[left]] = [heights[left], heights[i], names[left], names[i]];
        return i;
    };

    quickSort(0, heights.length - 1);
    return names;
};
```