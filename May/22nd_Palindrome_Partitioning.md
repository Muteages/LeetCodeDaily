# Palindrome Partitioning

https://leetcode.com/problems/palindrome-partitioning

Given a string s, partition s such that every substring of the partition is a palindrome. Return all possible palindrome partitioning of s.

## Approach 1

Backtracking 
``` C++
    std::vector<std::vector<std::string>> ans;
    bool isPalindrome(const std::string& s, int l, int r)
    {
        while (l < r)
        {
            if (s[l] != s[r])
            {
                return false;
            }
            l++;
            r--;
        }
        return true;
    }

    void getPalindrome(const std::string& s, std::vector<std::string>& curr, int left)
    {
        if (left == s.length())
        {
            ans.emplace_back(curr);
            return;
        }
        for (int right = left; right < s.length(); right++)
        {
            if (isPalindrome(s, left, right))
            {
                curr.emplace_back(s.substr(left, right - left + 1));
                getPalindrome(s, curr, right + 1);
                curr.pop_back();
            }
        }
    }

    vector<vector<string>> partition(string s) {
        std::vector<std::string> curr{};
        getPalindrome(s, curr, 0);
        return ans;
    }
```

## Approach 2 

Backtracking and DP

``` C++
    std::vector<std::vector<std::string>> ans;    
    std::vector<std::vector<bool>> dp;
    
    void initDP(const std::string& s)
    {
        int n = s.length();
        dp.resize(n, std::vector<bool>(n, false));
        for (int len = 1; len <= n; len++)
        {
            for (int left = 0; left <= n - len; left++)
            {
                int right = left + len - 1;
                dp[left][right] = (s[left] == s[right] && (len < 3 || dp[left + 1][right - 1]));
            }
        }
    }

    void getPalindrome(const std::string& s, std::vector<std::string>& curr, int left)
    {
        if (left == s.length())
        {
            ans.emplace_back(curr);
            return;
        }
        for (int right = left; right < s.length(); right++)
        {
            if (dp[left][right])
            {
                curr.emplace_back(s.substr(left, right - left + 1));
                getPalindrome(s, curr, right + 1);
                curr.pop_back();
            }
        }
    }

    vector<vector<string>> partition(string s) {
        initDP(s);
        std::vector<std::string> curr{};
        getPalindrome(s, curr, 0);
        return ans;
    }
```