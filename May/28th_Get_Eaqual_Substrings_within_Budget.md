# Get Eaqual Substirngs within Budget

https://leetcode.com/problems/get-equal-substrings-within-budget

## Approach 1

``` C++
    int equalSubstring(string s, string t, int maxCost) {
        int len = s.length(), left = 0, ans = 0;
        for (int right = 0; right < len; right++)
        {
            maxCost -= std::abs(s[right] - t[right]);
            while (maxCost < 0)
            {
                maxCost += std::abs(s[left] - t[left]);
                left++;
            }
            ans = std::max(ans, right - left + 1);
        }
        return ans;
    }
```