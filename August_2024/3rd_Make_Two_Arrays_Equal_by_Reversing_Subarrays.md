# Make Two Arrays Equal by Reversing Subarrays

You are given two integer arrays of equal length target and arr. In one step, you can select any non-empty subarray of arr and reverse it. You are allowed to make any number of steps.

Return true if you can make arr equal to target or false otherwise.

## Approach 

``` C++
    bool canBeEqual(vector<int>& target, vector<int>& arr) {
        int freq[1001] = {0};
        int MAX = 0;
        for (int i = 0; i < target.size(); i++)
        {
            freq[target[i]]++;
            freq[arr[i]]--;
            MAX = std::max({MAX, target[i], arr[i]});
        }
        for (int i = 0; i <= MAX; i++)
        {
            if (freq[i] != 0) return false;
        }
        return true;
    }
```

``` JavaScript
var canBeEqual = function(target, arr) {
    const freq = new Map();
    for (let i = 0; i < target.length; i++) {
        let a = target[i], b = arr[i];
        freq.set(a, (freq.get(a) || 0) + 1);
        freq.set(b, (freq.get(b) || 0) - 1);
    }

    for (const [num, f] of freq)
    {
        if (f !== 0) return false;
    }
    return true;
};
```