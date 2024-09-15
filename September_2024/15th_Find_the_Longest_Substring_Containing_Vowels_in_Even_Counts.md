# Find the Longest Substring Containing Vowels in Even Counts



## Approach 1

O(n^2)

``` C++
    int findTheLongestSubstring(string s) {
        std::string vowels = "aeiou";
        int len = s.length();
        std::vector<int> prefix(len + 1, 0);
        int XOR = 0;
        for (int i = 1; i <= len; i++)
        {
            if (vowels.find(s[i - 1]) != std::string::npos)
            {
                XOR ^= (1 << (s[i - 1] - 'a'));
            }
            prefix[i] = XOR;
        }

        int ans = 0;
        for (int i = 0; i <= len; i++)
        {
            for (int j = len; j > i; j--)
            {
                if (prefix[j] == prefix[i])
                {
                    ans = std::max(ans, j - i);
                    break;
                }
            }
        }
        return ans;
    }
```


## Approach 2

O(n) approach

``` C++
 int findTheLongestSubstring(string s) {
        std::string vowels = "aeiou";
        int len = s.length();
        std::unordered_map<int, int> occuriences;
        occuriences[0] = 0; // The empty string has no vowels, when we encounter 0 again, it means we have even counts of vowels.
        int XOR = 0, ans = 0;
        for (int i = 0; i < len; i++)
        {
            if (vowels.find(s[i]) != std::string::npos)
            {
                XOR ^= 1 << (s[i] - 'a');
            }
            if (occuriences.count(XOR))
            {
                ans = std::max(ans, i - occuriences[XOR] + 1);
            }
            else
            {
                occuriences[XOR] = i + 1; // Except current vowel to maintain the subarry has even counts of vowels
            }
        }
        return ans;
    }
```


``` C++
    int findTheLongestSubstring(string s) {
        std::vector<int> digits(26, -1);
        digits['a' - 'a'] = 0, digits['e' - 'a'] = 1, digits['i' - 'a'] = 2, digits['o' - 'a'] = 3, digits['u' - 'a'] = 4;
        int len = s.length();
        std::vector<int> occuriences(32, -1);
        occuriences[0] = 0; // The empty string has no vowels, when we encounter 0 again, it means we have even counts of vowels.
        int ans = 0, XOR = 0;
        for (int i = 0; i < len; i++)
        {
            int digit = digits[s[i] - 'a'];
            XOR ^= (digit == -1) ? 0 : (1 << digit);
            if (occuriences[XOR] == -1)
            {
                occuriences[XOR] = i + 1; // Except current vowel to maintain the subarry has even counts of vowels
            }
            ans = std::max(ans, i - occuriences[XOR] + 1);
        }
        return ans;
    }
```