# Find the Pivot Integer

https://leetcode.com/problems/find-the-pivot-integer

Given a positive integer n, find the pivot integer x such that:

The sum of all elements between 1 and x inclusively equals the sum of all elements between x and n inclusively.
Return the pivot integer x. If no such integer exists, return -1. It is guaranteed that there will be at most one pivot index for the given input.


## Approach 1

``` C++
    int pivotInteger(int n) {
        int pivot = n;
        int prefix{}, suffix{};
        while (pivot)
        {
            // Sn = n * (a1 + an) / 2
            prefix = pivot * (1 + pivot);
            suffix = (n - pivot + 1) * (pivot + n);
            if (prefix == suffix)
            {
                return pivot;
            }
            pivot -= 1;
        }
        return -1;
    }
```

## Approach 2
Same with Approach 1
``` C++
    int pivotInteger(int n) {
        int prefix = n * (1 + n) / 2;
        int pivot = n;
        int suffix = 0;
        while (pivot > n / 2)
        {
            suffix += pivot;
            if (prefix == suffix)
            {
                return pivot;
            }
            prefix -=pivot;
            pivot -= 1;
        }
        return -1;
    }
```

## Approach 3

``` C++
    int pivotInteger(int n) {
        double x = std::sqrt(n * (n + 1) / 2);
        return x == static_cast<int>(x) ? x : -1;
    }
```