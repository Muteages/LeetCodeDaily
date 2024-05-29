# Number of Steps to Reduce a Number in Binary Representation to One

https://leetcode.com/problems/number-of-steps-to-reduce-a-number-in-binary-representation-to-one

Given the binary representation of an integer as a string s, return the number of steps to reduce it to 1 under the following rules:

If the current number is even, you have to divide it by 2.

If the current number is odd, you have to add 1 to it.

It is guaranteed that you can always reach one for all test cases.


## Approach 

``` C++
    int numSteps(string s) {
        int n = s.length();
        int carry = 0, ans = n - 1; // at least we need to pop n - 1 digits to make the number to 1 
        for (int i = n - 1; i > 0; i--)
        {
            if ((s[i] - '0') + carry == 1)
            {
                carry = 1;
                ans++;
            }
        }
        if (carry)
        { // Indicates we need an extra digit to handle the orginal first digit
            ans += 1;
        }
        return ans;
    }
```