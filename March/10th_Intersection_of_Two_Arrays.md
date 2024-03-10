# Intersection of Two Arrays

Given two integer arrays nums1 and nums2, return an array of their intersection. Each element in the result must be unique and you may return the result in any order.

## Approach 1

Utilise hash set

``` C++
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        std::unordered_set<int> n1, n2;
        for (int num : nums1)
        {
            n1.insert(num);
        }
        for (int num : nums2)
        {
            n2.insert(num);
        }
        std::vector<int> ans;
        for (int num : n1)
        {
            if (n2.count(num))
            {
                ans.emplace_back(num);
            }
        }
        return ans;
    }
```

## Approach 2

Utilise an extra boolean vector to check numbers
``` C++
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        std::vector<bool> exist(1001, false);
        std::vector<int> ans;
        for (int num : nums1)
        {
            exist[num] = true;
        }
        for (int num : nums2)
        {
            if (exist[num] == true)
            {
                ans.emplace_back(num);
                exist[num] = false; // Remove duplicates
            }
        }
        return ans;
    }
```