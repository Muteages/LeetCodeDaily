# Reverse Prefix of Word

https://leetcode.com/problems/reverse-prefix-of-word/description

Given a 0-indexed string word and a character ch, reverse the segment of word that starts at index 0 and ends at the index of the first occurrence of ch (inclusive). If the character ch does not exist in word, do nothing.

For example, if word = "abcdefd" and ch = "d", then you should reverse the segment that starts at 0 and ends at 3 (inclusive). The resulting string will be "dcbaefd".
Return the resulting string.


## Approach 1

``` C++
    string reversePrefix(string word, char ch) {
        int pos = word.find(ch);
        if (pos != std::string::npos)
        {
            std::reverse(word.begin(), word.begin() + pos + 1);
            /*
            int left = 0;
            while (left < pos)
            {
                std::swap(word[left], word[pos]);
                left++;
                pos--;
            }
            */
        }
        return word;
    }
```

