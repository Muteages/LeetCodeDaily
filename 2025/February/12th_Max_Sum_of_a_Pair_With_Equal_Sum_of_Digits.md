# Max Sum of a Pair With Equal Sum of Digits

https://leetcode.com/problems/max-sum-of-a-pair-with-equal-sum-of-digits/description/

You are given a 0-indexed array nums consisting of positive integers. You can choose two indices i and j, such that i != j, and the sum of digits of the number nums[i] is equal to that of nums[j].

Return the maximum value of nums[i] + nums[j] that you can obtain over all possible indices i and j that satisfy the conditions. If no such pair of indices exists, return -1.

## Approach 

``` C++
    inline int getSum(int num)
    {
        int sum = 0;
        for (; num > 0; sum += num % 10, num /= 10);
        return sum;
    }

    int maximumSum(vector<int>& nums) {
        std::vector<int> sums(82, 0);
        int ans = -1;
        for (int num : nums)
        {
            int sum = getSum(num);
            if (sums[sum] > 0)
            {
                ans = std::max(ans, sums[sum] + num);
            }
            sums[sum] = std::max(sums[sum], num);
        }
        return ans;
    }
```

``` Python
    def maximumSum(self, nums: List[int]) -> int:
        def get_sum(num: int) -> int:
            s = 0
            while num > 0:
                q, r = divmod(num, 10)
                s += r
                num = q
            return s
        
        ans = -1
        sums = [0] * 82 # Max sum is 81
        for num in nums:
            curr = get_sum(num)
            if sums[curr] > 0:
                ans = max(ans, sums[curr] + num)
            sums[curr] = max(sums[curr], num)
        
        return ans
```

``` JavaScript
var maximumSum = function(nums) {
    const sums = new Array(82).fill(0);
    let ans = -1;
    for (let num of nums) {
        const sum = [...String(num)].reduce((acc, dig) => acc + Number(dig), 0);
        if (sums[sum] > 0) {
            ans = Math.max(ans, sums[sum] + num);
        }
        sums[sum] = Math.max(sums[sum], num);
    }
    return ans;
};
```

## Approach 2

``` C++
    inline int getSum(int num)
    {
        int sum = 0;
        while (num > 0)
        {
            sum += num % 10;
            num /= 10;
        }
        return sum;
    }

    int maximumSum(vector<int>& nums) {
        std::vector<std::pair<int, int>> freq(82, {0, 0}); // Record the max and second max number
        int minSum = 83, maxSum = 0;
        for (int num : nums)
        {
            int sum = getSum(num);
            minSum = std::min(minSum, sum);
            maxSum = std::max(maxSum, sum);
            auto& [a, b] = freq[sum];
            if (a == 0)
            {
                a = num;
            }
            else if (num >= a)
            {
                b = a;
                a = num;
            }
            else if (num > b)
            {
                b = num;
            }
        }

        int ans = -1;
        for (int sum = minSum; sum <= maxSum; sum++)
        {
            auto [a, b] = freq[sum];
            if (b == 0) continue;
            ans = std::max(ans, a + b);
        }
        return ans;
    }
```