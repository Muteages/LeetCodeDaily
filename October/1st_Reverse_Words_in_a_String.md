# Reverse Words in a String

https://leetcode.com/problems/reverse-words-in-a-string-iii

Given a string s, reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.

## Approach 

Use stringstream

``` C++
    string reverseWords(string s) {
        std::stringstream ss(s);
        std::string ans;
        std::string temp;
        while (ss >> temp)
        {
            std::reverse(temp.begin(), temp.end());
            ans.append(temp);
            ans.append(" ");
        }
        ans.pop_back();
        return ans;
    }
```

## Approach 2

Two pointers

``` C++
    string reverseWords(string s) {
        size_t st = 0;
        while (true)
        {
            size_t ed = s.find(" ", st);
            if (ed == std::string::npos)
            { // The last word
                std::reverse(s.begin() + st, s.end());
                break;
            }
            else
            {
                std::reverse(s.begin() + st, s.begin() + ed);
            }
            st = ed + 1;
        }
        return s;
    }
```