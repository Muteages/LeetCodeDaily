# Check if Array Pairs are Divisible by K

https://leetcode.com/problems/check-if-array-pairs-are-divisible-by-k

Given an array of integers arr of even length n and an integer k.

We want to divide the array into exactly n / 2 pairs such that the sum of each pair is divisible by k.

Return true If you can find a way to do that or false otherwise.

## Approach 

``` C++
    bool canArrange(vector<int>& arr, int k) {
        int n = arr.size();
        std::vector<int> freq(k, 0);
        for (int num : arr)
        {
            freq[((num % k) + k) % k]++; // (num % k) + k  convert negative number to coreesponding positive number
        }

        if ((freq[0] & 1) || (!(k & 1) && (freq[k / 2] & 1)))
        { // Edge case: for freq[0] and freq[i] where i == k - i, they must have even counts to make sure they can be paired
            return false;
        }
        for (int i = 1; i <= k / 2; i++)
        {
            if (freq[i] != freq[k - i])
            {
                return false;
            }
        }
        return true;
    }
```