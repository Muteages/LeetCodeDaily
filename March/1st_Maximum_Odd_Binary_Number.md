# Maximum Odd Binary Number

https://leetcode.com/problems/maximum-odd-binary-number

You are given a binary string s that contains at least one '1'.

You have to rearrange the bits in such a way that the resulting binary number is the maximum odd binary number that can be created from this combination.

Return a string representing the maximum odd binary number that can be created from the given combination.

Note that the resulting string can have leading zeros.


## Approach 1

Utilise two pointers method to build the string in place.

``` C++
    string maximumOddBinaryNumber(string s) {
        int i = 0, pivot = 0;
        int len = s.length();
        while (i < len)
        {
            /*
                if (s[i] == '1')
                {
                    if (i != pivot)
                    { // Get rid of swap function
                        s[i] = '0';
                        s[pivot] = '1';
                    }
                pivot++;
            */
            if (s[i] == '1')
            {
                std::swap(s[i], s[pivot]);
                pivot++;
            }
            i++;
        }

        if (pivot != len)
        {
            s[pivot - 1] = '0';
            s[len - 1] = '1';
        }
        return s;
    }
```
## Approach 2

Build a new string by counting numbers of one and zero

``` C++
    string maximumOddBinaryNumber(string s) {
        int numberOfOne = std::count(s.begin(), s.end(), '1');
        int numberOfZero = s.length() - numberOfOne;
        return std::string(numberOfOne - 1, '1') + std::string(numberOfZero, '0') + '1';
    }
```
