# Count Triplets That Can Form Two Arrays of Equal XOR

https://leetcode.com/problems/count-triplets-that-can-form-two-arrays-of-equal-xor

Given an array of integers arr.

We want to select three indices i, j and k where (0 <= i < j <= k < arr.length).

Let's define a and b as follows:

a = arr[i] ^ arr[i + 1] ^ ... ^ arr[j - 1]
b = arr[j] ^ arr[j + 1] ^ ... ^ arr[k]
Note that ^ denotes the bitwise-xor operation.

Return the number of triplets (i, j and k) Where a == b.

## Approach 1

Brute force

``` C++
    int countTriplets(vector<int>& arr) {
        const int n = arr.size();
        int ans = 0;
        for (int i = 0; i < n; i++)
        {
            int a = arr[i];
            for (int j = i + 1; j < n; j++)
            {
                a ^= arr[j];
                int b = arr[j];
                for (int k = j; k < n; k++)
                {
                    b ^= arr[k];
                    if (a == b)
                    {
                        ans++;
                    }
                }
            }
        }
        return ans;
    }
```

__a == b => a ^ b = 0 ==> arr[i] ^ arr[i + 1] ^ ... ^ arr[j - 1] ^ arr[j] ^ arr[j + 1] ^ ... ^ arr[k] = 0__


## Approach 2

``` C++
    int countTriplets(vector<int>& arr) {
        const int n = arr.size();
        std::vector<int> prefix(n + 1, 0);
        for (int i = 0; i < n; i++)
        {
            prefix[i + 1] = prefix[i] ^ arr[i];
        }
        int ans = 0;
        for (int i = 0; i < n; i++)
        {
            for (int k = i + 1; k < n; k++)
            {
                if (prefix[i] == prefix[k + 1])
                {
                    ans += (k - i);
                }
            }
        }
        return ans;
    }
```

## Approach 3

``` C++
    int countTriplets(vector<int>& arr) {
        const int n = arr.size();
        int ans = 0;
        for (int i = 0; i < n; i++)
        {
            int xorSum = 0;
            for (int k = i; k < n; k++)
            {
                xorSum ^= arr[k];
                if (xorSum == 0)
                {
                    ans += k - i;
                }
            }
        }
        return ans;
    }
```