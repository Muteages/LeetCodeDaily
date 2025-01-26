# Make Lexicographically Samllest Array by Swapping Elements

https://leetcode.com/problems/make-lexicographically-smallest-array-by-swapping-elements

You are given a 0-indexed array of positive integers nums and a positive integer limit.

In one operation, you can choose any two indices i and j and swap nums[i] and nums[j] if |nums[i] - nums[j]| <= limit.

Return the lexicographically smallest array that can be obtained by performing the operation any number of times.

An array a is lexicographically smaller than an array b if in the first position where a and b differ, array a has an element that is less than the corresponding element in b. For example, the array [2,10,3] is lexicographically smaller than the array [10,2,3] because they differ at index 0 and 2 < 10.




## Approach 

``` C++
    vector<int> lexicographicallySmallestArray(vector<int>& nums, int limit) {
        const int n = nums.size();
        std::vector<int> indices(n);
        std::iota(indices.begin(), indices.end(), 0); // Fill indices;
        std::sort(indices.begin(), indices.end(), [&](int l, int r) {
            return nums[l] < nums[r];
        });

        std::vector<std::vector<int>> groups{{indices[0]}};
        int prev = nums[indices[0]];
        for (int i = 1; i < n; i++)
        {
            int numIdx = indices[i], curr = nums[numIdx];
            if (curr - prev <= limit)
            { // Indicates current number is in the same group with the previous number
                groups.back().emplace_back(numIdx);
            }
            else
            {
                groups.push_back({numIdx});
            }
            prev = curr;
        }

        for (auto& group : groups)
        {
            int sz= group.size(), i = 0;
            std::vector<int> vals(sz);
            for (int numIdx : group)
            {
                vals[i++] = nums[numIdx];
            }

            std::sort(group.begin(), group.end());
            for (int i = 0; i < sz; i++)
            {
                nums[group[i]] = vals[i];
            }
        }
        return nums;
    }
```


``` Python
    def lexicographicallySmallestArray(self, nums: List[int], limit: int) -> List[int]:
        n = len(nums)
        indices = sorted(list(range(n)), key=lambda i : nums[i])

        groups = [[indices[0]]]
        prev = nums[indices[0]]

        for i in range(1, n):
            numIdx = indices[i]
            num = nums[numIdx]

            if num - prev <= limit:
                groups[-1].append(numIdx)
            else:
                groups.append([numIdx])
            
            prev = num
        
        for g in groups:
            vals = []
            for i in g:
                vals.append(nums[i])
            
            g.sort()

            for i in range(len(g)):
                nums[g[i]] = vals[i]

        return nums 
```

