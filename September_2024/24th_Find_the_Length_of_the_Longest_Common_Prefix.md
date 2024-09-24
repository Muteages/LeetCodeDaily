# Find the Length of the Longest Common Prefix

https://leetcode.com/problems/find-the-length-of-the-longest-common-prefix

You are given two arrays with positive integers arr1 and arr2.

A prefix of a positive integer is an integer formed by one or more of its digits, starting from its leftmost digit. For example, 123 is a prefix of the integer 12345, while 234 is not.

A common prefix of two integers a and b is an integer c, such that c is a prefix of both a and b. For example, 5655359 and 56554 have a common prefix 565 while 1223 and 43456 do not have a common prefix.

You need to find the length of the longest common prefix between all pairs of integers (x, y) such that x belongs to arr1 and y belongs to arr2.

Return the length of the longest common prefix among all pairs. If no common prefix exists among them, return 0.

## Approach 

``` C++
    inline int getLength(int num)
    {
        int len = 0;
        while (num > 0)
        {
            len++;
            num /= 10;
        }
        return len;
    }

    int longestCommonPrefix(vector<int>& arr1, vector<int>& arr2) {
        std::unordered_set<int> prefix{};
        for (int num : arr1)
        {
            while (num > 0)
            {
                prefix.emplace(num);
                num /= 10;
            }
        }

        int ans = 0;
        for (int num : arr2)
        {
            while (num > 0)
            {
                if (prefix.count(num))
                {
                    ans = std::max(ans, getLength(num));
                    break;
                }
                num /= 10;
            }
        }
        return ans;
    }
```

