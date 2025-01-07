# String Matching in An Array

https://leetcode.com/problems/string-matching-in-an-array

## Approach 1

Brute force

``` C++
    vector<string> stringMatching(vector<string>& words) {
        std::sort(words.begin(), words.end(), [](const std::string& w1, const std::string& w2){
            return w1.length() < w2.length();
        });

        int n = words.size();
        std::vector<std::string> ans{};
        for (int i = 0; i < n; i++)
        {
            for (int j = n - 1; j > i; j--)
            {
                if (words[j].find(words[i]) != std::string::npos)
                {
                    ans.emplace_back(words[i]);
                    break;
                }
            }
        }
        return ans; 
    }
```

## Approach 2

KMP

``` C++
    vector<string> stringMatching(vector<string>& words) {
        const int n = words.size();
        std::vector<std::string> ans{};
        for (const auto& pat : words)
        {
            // Build lps of current word
            std::vector<int> lps = buildLPS(pat);
            for (const auto& txt : words)
            {
                if (isSub(pat, txt, lps))
                {
                    ans.emplace_back(pat);
                    break;
                }
            }
        }
        return ans;
    }

    std::vector<int> buildLPS(const std::string& s)
    {
        std::vector<int> lps(s.length(), 0);
        int curIdx = 1, prefixIdx = 0;
        while (curIdx < lps.size())
        {
            if (s[curIdx] == s[prefixIdx])
            {
                lps[curIdx++] = ++prefixIdx;
            }
            else
            {
                if (prefixIdx > 0)
                {
                    prefixIdx = lps[prefixIdx - 1];
                }
                else
                {
                    curIdx++;
                }
            }
        }
        return lps;
    }

    bool isSub(const std::string& pat, const std::string& txt, const std::vector<int>& lps)
    {
        if (pat.length() >= txt.length())
        {
            return false;
        }

        int pIdx = 0, tIdx = 0;
        while (tIdx < txt.length())
        {
            if (pat[pIdx] == txt[tIdx])
            {
                pIdx++;
                tIdx++;
                if (pIdx == pat.length())
                {
                    return true;
                }
            }
            else
            {
                if (pIdx > 0)
                {
                    pIdx = lps[pIdx - 1];
                }
                else
                {
                    tIdx++;
                }
            }
        }
        return false;
    } 
```

