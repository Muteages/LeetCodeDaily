# Minimum Changes To Make Alternating Binary String

https://leetcode.com/problems/minimum-changes-to-make-alternating-binary-string

You are given a string s consisting only of the characters '0' and '1'. In one operation, you can change any '0' to '1' or vice versa.

The string is called alternating if no two adjacent characters are equal. For example, the string "010" is alternating, while the string "0100" is not.

Return the minimum number of operations needed to make s alternating.

## Approach 1

``` C++
    void flipBit(char& c)
    {
        c = c == '1' ? '0' : '1';
    }
    int minOperations(string s) {
        int pattern1 = 0; // 10101010
        char bit1 = '1';
        int pattern2 = 0; // 01010101
        char bit2 = '0';
        for (int i = 0; i < s.length(); i++)
        {
            pattern1 += s[i] == bit1;
            pattern2 += s[i] == bit2;
            flipBit(bit1);
            flipBit(bit2);
        }
        return std::min(pattern1, pattern2);
    }
```

## Approach 2

``` C++
    int minOperations(string s) {
        int op1 = 0; // 010101
        int op2 = 0; // 101010

        for (int i = 0; i < s.length(); i++)
        {
            if (i % 2 == 0)
            { // Even bit
                if (s[i] == '1')
                { // Convert it into 0
                    op1++;
                }
                else
                {
                    op2++;
                }
            }
            else
            {
                if (s[i] == '0')
                { // Convert it into 1
                    op1++;
                }
                else
                {
                    op2++;
                }
            }
        }
        return std::min(op1, op2);
    }
```