# Largest Number

https://leetcode.com/problems/largest-number

Given a list of non-negative integers nums, arrange them such that they form the largest number and return it.

Since the result may be very large, so you need to return a string instead of an integer.

## Approach 

``` C++
    string largestNumber(vector<int>& nums) {
        int n = nums.size();
        std::vector<std::string> ss(n);
        for (int i = 0; i < n; i++)
        {
            ss[i] = std::to_string(nums[i]);
        }

        std::sort(ss.begin(), ss.end(), [](const std::string& s1, const std::string& s2){
            return (s1.length() == s2.length()) ? s1 > s2 : s1 + s2 > s2 + s1;
        });

        if (ss[0] == "0")
        { // All numbers are 0
            return "0";
        }

        std::string ans{};
        for (const auto& s : ss)
        {
            ans += s;
        }
        return ans;
    }
```


``` JavaScript
var largestNumber = function(nums) {
    nums.sort((a, b) => `${b}${a}` - `${a}${b}`);
    if (nums[0] === 0) return "0";
    return nums.join('');
};
```
