# Find First Palindromic String in the Array

Given an array of strings words, return the first palindromic string in the array. If there is no such string, return an empty string "".

## Approach 

``` C++
    /*
    bool isPalindrome(const std::string& s)
    {
        int len = s.length();
        for (int i = 0; i < len; i++)
        {
            if (s[i] != s[len - 1 - i])
            {
                return false;
            }
        }
        return true;
    }
    */
    string firstPalindrome(vector<string>& words) {
        for (const auto& word : words)
        {
            auto temp = word;
            std::reverse(temp.begin(), temp.end());
            if (temp == word)
            {
                return word;
            }
            /*
            if (isPalindrome(word))
            {
                return word;
            }
            */
        }
        return "";
    }
```
