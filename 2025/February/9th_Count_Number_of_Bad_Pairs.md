# Count Number of Bad Pairs

https://leetcode.com/problems/count-number-of-bad-pairs

You are given a 0-indexed integer array nums. A pair of indices (i, j) is a bad pair if i < j and j - i != nums[j] - nums[i].

Return the total number of bad pairs in nums.


## Approach 

``` C++
    long long countBadPairs(vector<int>& nums) {
        const int n = nums.size();
        long long ans = (long long)n * (n - 1) / 2;
        std::unordered_map<int, int> pairs;
        for (int i = 0; i < n; i++)
        {
            int x = nums[i] - i;
            ans -= pairs[x];
            pairs[x]++;
        }
        return ans;
    }
```

``` Python
    def countBadPairs(self, nums: List[int]) -> int:
        n = len(nums)
        pairs = defaultdict(int)
        ans = n * (n - 1) // 2
        for i, num in enumerate(nums):
            x = num - i
            ans -= pairs[x]
            pairs[x] += 1
        return ans
```

``` Python
    def countBadPairs(self, nums: List[int]) -> int:
        count = Counter([num - i for i, num in enumerate(nums)])
        n = len(nums)
        ans = n * (n - 1) // 2
        return ans - sum(f * (f - 1) // 2 for f in count.values())
```