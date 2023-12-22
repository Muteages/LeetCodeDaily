# Maximum Score After Splitting a String

https://leetcode.com/problems/maximum-score-after-splitting-a-string

Given a string s of zeros and ones, return the maximum score after splitting the string into two non-empty substrings (i.e. left substring and right substring).

The score after splitting a string is the number of zeros in the left substring plus the number of ones in the right substring.

## Approach 

``` C++
    int maxScore(string s) {
        int l = s.length();
        std::vector<int> numOfOne(l, 0);
        for (int i = l - 2; i >= 0; i--)
        { // Count the number of one from right to left
            numOfOne[i] = (s[i + 1] == '1')   + numOfOne[i + 1];
        }

        int numOfZero = 0;
        int ans = 0;
        for (int i = 0; i < l - 1; i++)
        { // We must split s into two parts thus i < l - 1
            if (s[i] == '0')
            { // Count the number of zero first 
                numOfZero++;
            }
            ans = std::max(ans, numOfZero + numOfOne[i]);
        }
        return ans;
    }
```