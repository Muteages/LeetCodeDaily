# Number of Sub-arrays With Odd Sum

Given an array of integers arr, return the number of subarrays with an odd sum.

Since the answer can be very large, return it modulo 109 + 7.


## Approach 

``` C++
    int numOfSubarrays(vector<int>& arr) {
        const int MOD = 1e9 + 7;
        long long ans = 0;
        
        int isOdd = 0, evenCnt = 1, oddCnt = 0;
        for (int num : arr)
        {
            isOdd ^= (num & 1);
            if (isOdd)
            {
                ans += evenCnt;
                oddCnt++;
            }   
            else
            {
                ans += oddCnt;
                evenCnt++;
            }
        }

        /*  Alternatively, use 2-len array to avoid if conditions
        int cnt[2] = {1, 0}; // 0: even sum cnt, 1: odd sum cnt
        for (int num : arr)
        {
            isOdd ^= (num & 1);
            ans += cnt[1 - isOdd];
            cnt[isOdd]++;
        }
        */
        return ans % MOD;
    }
```

``` Python
    def numOfSubarrays(self, arr: List[int]) -> int:
        ans = 0
        isOdd = 0
        cnt = [1, 0] # cnt of even sum and odd sum
        for num in arr:
            isOdd ^= (num & 1)
            ans += cnt[1 - isOdd]
            cnt[isOdd] += 1
        
        return ans%(10**9+7)
``` 


``` JavaScript
var numOfSubarrays = function(arr) {
    const cnt = [1, 0];
    let isOdd = 0;
    let ans = 0;
    for (let num of arr) {
        isOdd ^= (num & 1);
        ans += cnt[1 - isOdd];
        cnt[isOdd]++;
    }
    return ans % (1e9 + 7);
};
```