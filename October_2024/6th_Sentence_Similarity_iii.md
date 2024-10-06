# Sentence Similarity III

https://leetcode.com/problems/sentence-similarity-iii

You are given two strings sentence1 and sentence2, each representing a sentence composed of words. A sentence is a list of words that are separated by a single space with no leading or trailing spaces. Each word consists of only uppercase and lowercase English characters.

Two sentences s1 and s2 are considered similar if it is possible to insert an arbitrary sentence (possibly empty) inside one of these sentences such that the two sentences become equal. Note that the inserted sentence must be separated from existing words by spaces.

For example,

s1 = "Hello Jane" and s2 = "Hello my name is Jane" can be made equal by inserting "my name is" between "Hello" and "Jane" in s1.
s1 = "Frog cool" and s2 = "Frogs are cool" are not similar, since although there is a sentence "s are" inserted into s1, it is not separated from "Frog" by a space.
Given two sentences sentence1 and sentence2, return true if sentence1 and sentence2 are similar. Otherwise, return false.


## Approach 1

Use stringstream or string_view to split sentence
``` C++
    std::vector<std::string> splitSentece(const std::string& sentence)
    {
        std::stringstream ss(sentence);
        std::vector<std::string> s;
        s.reserve(100);
        std::string temp{};
        while (ss >> temp)
        {
            s.emplace_back(std::move(temp));
        }
        return s;
    }

    /*
    std::vector<std::string_view> splitSentece(const std::string& sentence)
    {
        std::string_view sv(sentence);
        std::vector<std::string_view> s{};
        s.reserve(100);
        int l = 0, r = 0, n = sv.size();
        while (r <= n)
        {
            if (sv[r] == ' ' || r == n)
            {
                s.emplace_back(sv.substr(l, r - l));
                l = r + 1;
            }
            r++;
        }
        return s;
    }
    */

    bool areSentencesSimilar(string sentence1, string sentence2) {

        auto s1 = splitSentece(sentence1);
        auto s2 = splitSentece(sentence2);

        if (s1.size() > s2.size())
        {
            std::swap(s1, s2);
        }
        int prefixCnt = 0;
        int n1 = s1.size(), n2 = s2.size();
        for (int i = 0; i < n1; i++)
        {
            if (s1[i] != s2[i]) break;
            prefixCnt++;
        }
        if (prefixCnt == n1) return true;
        int suffixCnt = 0;
        // i1 >= prefixCnt, just in case there are two same words in the smaller string and recount the common prefix
        for (int i1 = n1 - 1, i2 = n2 - 1; i1 >= prefixCnt; i1--, i2--)
        {
            if (s1[i1] != s2[i2]) break;
            suffixCnt++;
        }
        return (prefixCnt + suffixCnt) == n1;
    }
```

## Approach 2

