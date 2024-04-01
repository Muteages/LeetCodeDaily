# Length of Last Word

Given a string s consisting of words and spaces, return the length of the last word in the string.

## Approach 1

``` C++
    int lengthOfLastWord(string s) {
        int len = s.length();
        int idx = len - 1;
        while (idx >= 0 && !std::isalpha(s[idx]))
        { // Find the fisrt letter in reverse order
            idx--;
        }
        int length = 0;
        while (idx >= 0 && std::isalpha(s[idx]))
        { // Find the first space before the last word
            length++;
            idx--;
        }
        return length;
    }
```

## Approach 2

Utilise std::string built-in functions.
``` C++
    int lengthOfLastWord(string s) {
        size_t right = s.find_last_not_of(' ');
        size_t left = s.find_last_of(' ', right);
        return left == std::string::npos ? right + 1 : right - left;
    }
```