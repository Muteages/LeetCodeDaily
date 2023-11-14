# Unique Length-3 Palindromic Subsequences

https://leetcode.com/problems/unique-length-3-palindromic-subsequences

Given a string s, return the number of unique palindromes of length three that are a subsequence of s.

Note that even if there are multiple ways to obtain the same subsequence, it is still only counted once.

## Approach 

``` C++
    int countPalindromicSubsequence(string s) {
        int left = 0;
        int ans = 0;
        std::set<char> usedHead; // Unique characters used at head and tail
        while (left <= (s.length() - 3)) // we need to have at least 3 characters
        {
            int right = s.length() - 1;
            std::set<char> usedMid; // Unique characters used at middle
            while ((right >= (left + 2)) && s[left] != s[right])
            { // Find the same head and tail first
                right--;
            }
            usedHead.insert(s[left]);
            for (int i = left + 1; i < right; i++)
            { // Update mid
                if (!usedMid.count(s[i]))
                {
                    ans++;
                    usedMid.insert(s[i]);
                }
                if (usedMid.size() == 26)
                {
                    break;
                }
            }

            while (left <= (s.length() - 3) && usedHead.count(s[left]))
            { // Update left
                left++;
            }
        }
        return ans;
    }
```

## Approach 2

``` C++
    int countPalindromicSubsequence(string s) {
        // Store the character minimum and maximum occurrences in the string
        std::vector<int> leftmost(26, INT_MAX);
        std::vector<int> rightmost(26, INT_MIN);

        for (int i = 0; i < s.length(); i++)
        {
            int curr = s[i] - 'a';
            leftmost[curr] = std::min(leftmost[curr], i);
            rightmost[curr] = std::max(rightmost[curr], i);
        }

        int ans = 0;
        for (int i = 0; i < 26; i++)
        {
            if (leftmost[i] == INT_MAX || rightmost[i] == INT_MIN)
            { // Can't build a palindromic
                continue;
            }

            std::unordered_set<char> count; // Record the unique characters in the middle position
            for (int j = leftmost[i] + 1; j < rightmost[i]; j++)
            {
                count.insert(s[j]);
            }

            ans += count.size();
        }
        return ans;
    }
```