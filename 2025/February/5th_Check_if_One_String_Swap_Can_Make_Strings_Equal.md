# Check if One String Swap Can Make Strings Equal

https://leetcode.com/problems/check-if-one-string-swap-can-make-strings-equal

You are given two strings s1 and s2 of equal length. A string swap is an operation where you choose two indices in a string (not necessarily different) and swap the characters at these indices.

Return true if it is possible to make both strings equal by performing at most one string swap on exactly one of the strings. Otherwise, return false.


## Approach 

``` C++
    bool areAlmostEqual(string s1, string s2) {
        if (s1 == s2) return true;
        int cnt = 0;
        std::string d1{}, d2{};
        for (int i = 0; i < s1.length(); i++)
        {
            if (s1[i] != s2[i])
            {
                cnt++;      
                d1 += s1[i];
                d2 += s2[i];
                if (cnt > 2) return false;
            }
        }
        return cnt == 2 && d1[0] == d2[1] && d1[1] == d2[0];
    }
```


``` Python
    def areAlmostEqual(self, s1: str, s2: str) -> bool:
        if s1 == s2:
            return True
        diffs = [(a, b) for a, b in zip(s1, s2) if a != b]
        return len(diffs) == 2 and diffs[0] == diffs[1][::-1]
```

``` JavaScript
var areAlmostEqual = function(s1, s2) {
    if (s1 === s2) return true;
    let diff = [];
    for (let i = 0; i < s1.length; i++) {
        if (s1[i] !== s2[i]) {
            diff.push([s1[i], s2[i]]);
            if (diff.length > 2) return false;
        }
    }
    return diff.length === 2 && diff[0][0] === diff[1][1] && diff[0][1] === diff[1][0];
};
```