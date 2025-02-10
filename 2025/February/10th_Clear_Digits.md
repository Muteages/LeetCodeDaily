# Clear Digits

https://leetcode.com/problems/clear-digits

## Approach 

``` C++
    string clearDigits(string s) {
        int i = 0;
        for (char ch : s)
        {
            if (std::isdigit(ch) && i > 0)
            {
                i--;
            }
            else
            {
                s[i++] = ch;
            }
        }
        s.resize(i);
        return s;
    }
```

``` Python
    def clearDigits(self, s: str) -> str:
        ans = []
        for ch in s:
            if ans and ch.isdigit():
                ans.pop()
            else:
                ans.append(ch)
        return "".join(ans)
```

``` JavaScript
var clearDigits = function(s) {
    let ans = "";
    for (const ch of s) {
        if (/\d/.test(ch) && ans.length > 0) {  // isNaN()
            ans = ans.slice(0, -1);
        } else {
            ans += ch;
        }
    }
    return ans;
};
```