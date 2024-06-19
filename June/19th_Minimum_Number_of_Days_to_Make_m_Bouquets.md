# Minimum Number of Days to Make m Bouquets

https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets

You are given an integer array bloomDay, an integer m and an integer k.

You want to make m bouquets. To make a bouquet, you need to use k adjacent flowers from the garden.

The garden consists of n flowers, the ith flower will bloom in the bloomDay[i] and then can be used in exactly one bouquet.

Return the minimum number of days you need to wait to be able to make m bouquets from the garden. If it is impossible to make m bouquets return -1.


## Approach

``` C++
    bool canMakeBouquets(vector<int>& bloomDay, int threshold, int m, int k)
    {
        int bouquets = 0, flowerCnt = 0;
        for (int f : bloomDay)
        {
            if (f <= threshold)
            {
                flowerCnt++;
                if (flowerCnt == k)
                { // Enable to assemble a bouquet
                    bouquets++;
                    flowerCnt = 0;
                }
            }
            else
            {
                flowerCnt = 0;
            }
            if (bouquets >= m)
            { // Collect enough bouquets
                break;
            }
        }
        return bouquets >= m;
    }


    int minDays(vector<int>& bloomDay, int m, int k) {
        if (static_cast<long long>(m) * k > bloomDay.size())
        {
            return -1;
        }

        auto lr = std::minmax_element(bloomDay.begin(), bloomDay.end());
        int left = *lr.first, right = *lr.second, mid{};
        while (left <= right)
        {
            mid = left + (right - left) / 2;
            if (canMakeBouquets(bloomDay, mid, m, k))
            {
                right = mid - 1;
            }
            else
            {
                left = mid + 1;
            }
        }
        return left;
    }
```


``` JavaScript
const canMakeBouquets = (bloom, t, m, k) => {
    let bouquets = 0, flowers = 0;
    for (let b of bloom) {
        if (b <= t) {
            flowers++;
            if (flowers === k) {
                bouquets++;
                flowers = 0;
            }
        }
        else {
            flowers = 0;
        }

        if (bouquets >= m) {
            return true;
        }
    }
    return false;
};

var minDays = function(bloomDay, m, k) {
    const flowers = bloomDay.length;
    const required = m * k;
    if (flowers < required) {
        return -1;
    }

    let left = Math.min(...bloomDay), right = Math.max(...bloomDay);
    while (left <= right) {
        let mid = Math.floor(left + (right - left) / 2);
        if (canMakeBouquets(bloomDay, mid, m, k)) {
            right = mid - 1;
        }
        else {
            left = mid + 1;
        }
    }
    return left;
};
```