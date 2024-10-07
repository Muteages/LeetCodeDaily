# Minimum String Length After Removing Substrings

https://leetcode.com/problems/minimum-string-length-after-removing-substrings

You are given a string s consisting only of uppercase English letters.

You can apply some operations to this string where, in one operation, you can remove any occurrence of one of the substrings "AB" or "CD" from s.

Return the minimum possible length of the resulting string that you can obtain.

Note that the string concatenates after removing the substring and could produce new "AB" or "CD" substrings.

## Approach 1

``` JavaScript
var minLength = function(s) {
    const st = [];
    for (let i = 0; i < s.length; i++) {
        if (st.length !== 0 && ((st.at(-1) === 'A' && s[i] === 'B') || (st.at(-1) === 'C' && s[i] === 'D'))) {
            st.pop();
        }
        else {
            st.push(s[i]);
        }
    }
    return st.length;
};
```

## Approach 2

Remove extra array, modify the string in place.

``` JavaScript
var minLength = function(s) {
    let arr = s.split('');  
    let sz = 1;
    
    for (let i = 1; i < arr.length; i++) {
        arr[sz] = arr[i];
        if (sz > 0 && ((arr[sz - 1] === 'A' && arr[i] === 'B') || 
                       (arr[sz - 1] === 'C' && arr[i] === 'D'))) {
            sz--;
        } else {
            sz++;
        }
    }
    return sz;
};
```
