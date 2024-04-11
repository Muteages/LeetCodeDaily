# Remove K Digits

https://leetcode.com/problems/remove-k-digits

Given string num representing a non-negative integer num, and an integer k, return the smallest possible integer after removing k digits from num.

## Approach 1

``` C++
    string removeKdigits(string num, int k) {
        int len = num.length();
        if (len == k)
        {
            return "0";
        }

        std::string ans{};
        for (const char& ch : num)
        {
            while (!ans.empty() && ch < ans.back() && k > 0)
            { // Check if the last digit number is smaller than current numebr
                ans.pop_back();
                k--;
            }
            ans += ch;
        }
        
        while (k > 0)
        {
            ans.pop_back();
            k--;
        }
        int i = 0;
        while(ans[i] == '0')
        { // Remove leading zero
            i++;
        }
        return (i == ans.size()) ? "0" : ans.substr(i);
    }
```

## Approach 2

Rewrite string in place

``` C++
    string removeKdigits(string num, int k) {
        int len = num.length();
        if (len == k)
        {
            return "0";
        }
        int rewrite = 0;
        for (const char& ch : num)
        {
            while (rewrite > 0 && ch < num[rewrite - 1] && k > 0)
            {
                rewrite--;
                k--;
            }
            num[rewrite++] = ch;
        }
        
        while (k > 0)
        {
            rewrite--;
            k--;
        }
        num.resize(rewrite);
        int i = 0;
        while(num[i] == '0')
        { // Remove leading zero
            i++;
        }
        num.erase(num.begin(), num.begin() + i);
        return num.empty() ? "0" : num;
    }
```