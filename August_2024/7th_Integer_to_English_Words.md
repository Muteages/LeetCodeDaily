# Integer to English Words

https://leetcode.com/problems/integer-to-english-words

Convert a non-negative integer num to its English words representation.

 
## Approach 

``` C++
    std::string eng1[20] = {
        "",        "One",       "Two",      "Three",
        "Four",    "Five",      "Six",      "Seven",
        "Eight",   "Nine",      "Ten",      "Eleven",
        "Twelve",  "Thirteen",  "Fourteen", "Fifteen",
        "Sixteen", "Seventeen", "Eighteen", "Nineteen"
    };

    std::string eng2[10] = {
        "",      "Ten",   "Twenty",  "Thirty", "Forty",
        "Fifty", "Sixty", "Seventy", "Eighty", "Ninety"
    };

    std::string eng3[4] = {"", "Thousand", "Million", "Billion"};

    string numberToWords(int num) {
        if (num == 0) return "Zero";

        std::string ans{};
        int cnt = 0;
        while (num > 0)
        {
            auto [q, r] = std::div(num, 1000);
            num = q;
            if (r > 0)
            {
                std::string temp = convert(r) + " " + eng3[cnt];
                ans = ans.empty() ? temp : temp + " " + ans;
            }
            cnt++;
        }

        if (!ans.empty() && ans.back() == ' ') ans.pop_back();
        return ans;
    }

    std::string convert(int num)
    {
        std::string s{};
        if (num >= 100)
        {
            auto [q, r] = std::div(num, 100);
            s += eng1[q] + " Hundred ";
            num = r;
        }
        
        if (num >= 20)
        {
            auto [q, r] = std::div(num, 10);
            s += eng2[q] + " " + eng1[r];
        }
        else
        {
            s += eng1[num];
        }

        if (!s.empty() && s.back() == ' ') s.pop_back();
        return s;
    }
```