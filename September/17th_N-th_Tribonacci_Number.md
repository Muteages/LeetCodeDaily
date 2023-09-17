# N-th Tribonacci Number

https://leetcode.com/problems/n-th-tribonacci-number/description

The Tribonacci sequence Tn is defined as follows: 

T0 = 0, T1 = 1, T2 = 1, and Tn+3 = Tn + Tn+1 + Tn+2 for n >= 0.

Given n, return the value of Tn.


## Approach 

``` C++
    int tribonacci(int n) {
        if (n == 0)
        {
            return 0;
        }
        if (n == 1 || n == 2)
        {
            return 1;
        }
        std::vector<int> nums(n + 1, 1); 
        nums[0] = 0;
        for (int curr = 3; curr <= n; curr++)
        {
            nums[curr] = nums[curr - 3] + nums[curr - 2] + nums[curr - 1];
            curr++;
        }
        return nums[n];
    }
```

