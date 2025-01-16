# Bitwise XOR of All Pairings

https://leetcode.com/problems/bitwise-xor-of-all-pairings

You are given two 0-indexed arrays, nums1 and nums2, consisting of non-negative integers. There exists another array, nums3, which contains the bitwise XOR of all pairings of integers between nums1 and nums2 (every integer in nums1 is paired with every integer in nums2 exactly once).

Return the bitwise XOR of all integers in nums3.


## Approach 

``` C++
    int XOR(const std::vector<int>& nums, int cnt)
    {
        int ans = 0;
        if (cnt & 1)
        {
            ans = std::accumulate(nums.begin(), nums.end(), 0, bit_xor<int>());
        }
        return ans;
    }

    int xorAllNums(vector<int>& nums1, vector<int>& nums2) {
        const int n1 = nums1.size(), n2 = nums2.size();
        return XOR(nums1, n2) ^ XOR(nums2, n1);
    }
```

``` JavaScript
var xorAllNums = function(nums1, nums2) {   
    const n1 = nums1.length, n2 = nums2.length;
    
    const xor = (nums, cnt) => {
        if (!(cnt & 1)) return 0;

        let ans = 0;
        nums.forEach((num) => ans ^= num);
        return ans;
    };

    return xor(nums1, n2) ^ xor(nums2, n1);
};
```

``` Python
    def xorAllNums(self, nums1: List[int], nums2: List[int]) -> int:
        def xor(nums: List[int], cnt: int) -> int:
            if not(cnt & 1):
                return 0
            else:
                return reduce(ixor, nums)    

        n1 = len(nums1)
        n2 = len(nums2)
        return xor(nums1, n2) ^ xor(nums2, n1)
```

