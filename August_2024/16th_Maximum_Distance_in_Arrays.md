# Maximum Distance in Arrays

https://leetcode.com/problems/maximum-distance-in-arrays/

You are given m arrays, where each array is sorted in ascending order.

You can pick up two integers from two different arrays (each array picks one) and calculate the distance. We define the distance between two integers a and b to be their absolute difference |a - b|.

Return the maximum distance.

## Approach 1

``` C++
    int maxDistance(vector<vector<int>>& arrays) {
        const int n = arrays.size();
        int biggest{INT_MIN}, secondBiggest{INT_MIN}, smallest{INT_MAX}, secondSmallest{INT_MAX},
            biggestIdx{-1}, secondBiggestIdx{-1}, smallestIdx{-1}, secondSmallestIdx{-1};
        for (int i = 0; i < n; i++)
        {
            int curMin{arrays[i].front()}, curMax{arrays[i].back()};
            if (curMin < smallest)
            {
                secondSmallest = smallest;
                secondSmallestIdx = smallestIdx;
                smallest = curMin;
                smallestIdx = i;
            }
            else if (curMin < secondSmallest)
            {
                secondSmallest = curMin;
                secondSmallestIdx = i;
            }
            if (curMax > biggest)
            {
                secondBiggest = biggest;
                secondBiggestIdx = biggestIdx;
                biggest = curMax;
                biggestIdx = i;
            }
            else if (curMax > secondBiggest)
            {
                secondBiggest = curMax;
                secondBiggestIdx = i;
            }
        }
        return biggestIdx == smallestIdx ? std::max(biggest - secondSmallest, secondBiggest - smallest) : biggest - smallest;
    }
```

## Approach 2

``` C++
    int maxDistance(vector<vector<int>>& arrays) {
        int n = arrays.size(), maxDist = 0,
            minEle = 1e5, maxEle = -1e5;
        
        for (const auto& array : arrays)
        {
            int curMin = array.front(), curMax = array.back();
            maxDist = std::max({maxDist, curMax - minEle, maxEle - curMin});
            minEle = std::min(minEle, curMin);
            maxEle = std::max(maxEle, curMax);
        }
        return maxDist;
    }
```