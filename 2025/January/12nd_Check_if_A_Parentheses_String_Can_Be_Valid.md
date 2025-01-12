# Check if a Parentheses String Can Be Valid

https://leetcode.com/problems/check-if-a-parentheses-string-can-be-valid

A parentheses string is a non-empty string consisting only of '(' and ')'. It is valid if any of the following conditions is true:

It is ().
It can be written as AB (A concatenated with B), where A and B are valid parentheses strings.
It can be written as (A), where A is a valid parentheses string.
You are given a parentheses string s and a string locked, both of length n. locked is a binary string consisting only of '0's and '1's. For each index i of locked,

If locked[i] is '1', you cannot change s[i].
But if locked[i] is '0', you can change s[i] to either '(' or ')'.
Return true if you can make s a valid parentheses string. Otherwise, return false.

## Approach 

``` C++
    bool canBeValid(string s, string locked) {
        int n = s.size();
        if ((n & 1) || (s[0] == ')' && locked[0] == '1') || (s[n - 1] == '(' && locked[n - 1] == '1')) return false;

        int openNeeded = 0, closeNeeded = 0;
        
        for (int left = 0; left < n; left++)
        {
            int right = n - 1 - left;
            if (locked[left] == '0')
            {
                openNeeded--;
            }
            else
            {
                openNeeded += s[left] == ')' ? 1 : -1;
            }

            if (locked[right] == '0')
            {
                closeNeeded--;
            }
            else
            {
                closeNeeded += s[right] == '(' ? 1 : -1;
            }

            if (openNeeded > 0 || closeNeeded > 0)
            {
                return false;
            }

        }
        return true;
    }
```

``` Python
    def canBeValid(self, s: str, locked: str) -> bool:
        n = len(s)
        if (n & 1) or (s[0] == ')' and locked[0] == '1') or (s[-1] == '(' and locked[-1] == '1'):
            return False
        
        open_needed = 0
        close_needed = 0

        for left in range(n):
            right = n - 1 - left
            if locked[left] == '0':
                open_needed -= 1
            else:
                open_needed += 1 if s[left] == ')' else -1
            
            if locked[right] == '0':
                close_needed -= 1
            else:
                close_needed += 1 if s[right] == '(' else -1
            
            if open_needed > 0 or close_needed > 0:
                return False
        
        return True
```