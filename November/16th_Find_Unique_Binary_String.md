# Find Unique Binary String

https://leetcode.com/problems/find-unique-binary-string

Given an array of strings nums containing n unique binary strings each of length n, return a binary string of length n that does not appear in nums. If there are multiple answers, you may return any of them.

## Approach 

Cantor's diagonal

``` C++
    string findDifferentBinaryString(vector<string>& nums) {
        std::string ans = "";
        for (int i = 0; i < nums.size(); i++)
        {
            ans += nums[i][i] == '0' ? '1' : '0';
        }
        return ans;
    }
```

## Approach 2

Bitset with extra space
``` C++
    string findDifferentBinaryString(vector<string>& nums) {
        std::unordered_set<size_t> us; // Store all exist number
        for (auto& num : nums)
        {
            us.insert(std::bitset<16>(num).to_ulong());
        }

        int n = nums.size();
        for (size_t i = 0; i < std::pow(2, n + 1) - 1; i++)
        {
            if (!us.count(i))
            {
                return std::bitset<16>(i).to_string().substr(16 - n);
            }
        }
        return "";
    }
```

## Approach 3

Bitset with sort
``` C++
    string findDifferentBinaryString(vector<string>& nums) {
        std::sort(nums.begin(), nums.end());

        int candidate = 0;
        int n = nums.size();

        for (int i = 0; i < n; i++)
        {
            int integer = std::bitset<16>(nums[i]).to_ulong();
            if (candidate == integer)
            { // Find the number, go to check next
                candidate++;
            }
            else
            {
                break;
            }
        }
        return std::bitset<16>(candidate).to_string().substr(16 - n);
    }
```