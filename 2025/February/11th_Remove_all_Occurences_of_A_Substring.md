# Remove All Occurrences of a Substring

https://leetcode.com/problems/remove-all-occurrences-of-a-substring

Given two strings s and part, perform the following operation on s until all occurrences of the substring part are removed:

Find the leftmost occurrence of the substring part and remove it from s.
Return s after removing all occurrences of part.

A substring is a contiguous sequence of characters in a string.

## Approach 

``` C++

    /*
    bool isMatch(const std::string& s, const std::string& part)
    {
        int sl = s.length(), pl = part.length();
        if (sl < pl) return false;
        for (int si = sl - 1, pi = pl - 1; pi >= 0; pi--, si--)
        {
            if (s[si] != part[pi]) return false;
        }
        return true;
    }
    */


    string removeOccurrences(string s, string part) {
        const int sl = s.length(), pl = part.length();
        int idx = 0;
        // Alternatively, create an extra string and use ends_with()
        for (char ch : s)
        {
            s[idx++] = ch;
            if (idx >= pl && std::equal(s.begin() + idx - pl, s.begin() + idx, part.begin()))
            {
                idx -= pl;
            }
        }
        s.resize(idx);
        return s;
    }
```

``` Python
    def removeOccurrences(self, s: str, part: str) -> str:
        pl, idx = len(part), 0
        ans = ''
        for ch in s:
            ans += ch
            idx += 1
            if idx >= pl and ans.endswith(part):
                idx -= pl
                ans = ans[0:idx]
        return ans
```

``` JavaScript
var removeOccurrences = function(s, part) {
    const pl = part.length;
    let ans = [];
    for (ch of s) {
        ans.push(ch);
        if (ans.length >= pl && ans.slice(-pl).join('') === part) {
            ans.length -= pl;
        }
    }
    return ans.join('');
};
```

## Approach 2

``` C++
    string removeOccurrences(string s, string part) {
        int pl = part.length();
        while (s.length() > 0 && s.find(part) != -1)
        {
            s.erase(s.find(part), pl);
        }
        return s;
    }
```


``` JavaScript
var removeOccurrences = function(s, part) {
    const pl = part.length;
    while (s.includes(part)) {
        s = s.replace(part, '');
    }
    return s;
};
```
