# Tuple with the same product

https://leetcode.com/problems/tuple-with-same-product

Given an array nums of distinct positive integers, return the number of tuples (a, b, c, d) such that a * b = c * d where a, b, c, and d are elements of nums, and a != b != c != d.

## Approach 

``` C++
    int tupleSameProduct(vector<int>& nums) {
        const int n = nums.size();
        std::vector<int> products{};
        products.reserve(n * (n - 1) / 2);
        for (int i = 0; i < n; i++)
        {
            for (int j = i + 1; j < n; j++)
            {
                products.emplace_back(nums[i] * nums[j]);
            }
        }
        std::sort(products.begin(), products.end());
        
        int ans = 0;
        int prev = products[0], cnt = 1;
        for (int i = 1; i < products.size(); i++)
        {
            if (products[i] == prev)
            {
                cnt++;
            }
            else
            {
                ans += cnt * (cnt - 1) * 4; // cnt * (cnt - 1) / 2 * 8
                cnt = 1;
                prev = products[i];
            }
        }
        return ans;
    }
```

``` Python
    def tupleSameProduct(self, nums: List[int]) -> int:
        n = len(nums)
        freq = defaultdict(int)
        for x, y in combinations(nums, 2):
            freq[x * y] += 1
        
        return sum(f * (f - 1) * 4 for f in freq.values())
```

``` JavaScript
var tupleSameProduct = function(nums) {
    const freq = new Map();
    const n = nums.length;
    for (let i = 0; i < n; i++) {
        for (let j = i + 1; j < n; j++) {
            const p = nums[i] * nums[j];
            freq.set(p, (freq.get(p) || 0) + 1);
        }
    }

    let ans = 0;
    for (let f of freq.values()) {
        ans += f * (f - 1) * 4;
    }
    return ans;
};
```

