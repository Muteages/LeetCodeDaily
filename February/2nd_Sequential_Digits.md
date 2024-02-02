# Sequential Digits

https://leetcode.com/problems

An integer has sequential digits if and only if each digit in the number is one more than the previous digit.

Return a sorted list of all the integers in the range [low, high] inclusive that have sequential digits.


## Approach 1

``` C++
    vector<int> sequentialDigits(int low, int high) {
        int minL = std::to_string(low).length();
        int maxL = std::to_string(high).length();
        std::vector<int> ans;
        for (int curLen = minL; curLen <= maxL; curLen++)
        { // Trverse each possiable length
            for (int highestBitNum = 1; highestBitNum <= 9 - curLen + 1; highestBitNum++)
            { // From the highest bit, build the number
                int curBitNum = highestBitNum;
                int temp{};
                for (int curBit = curLen; curBit > 0; curBit--)
                { // Calculate each bit
                    temp += curBitNum * std::pow(10, curBit - 1);
                    curBitNum++;
                }
                if (temp > high)
                { // Prevent from doing unecessary iteration
                    return ans;
                }
                if (temp >= low && temp <= high)
                {
                   ans.emplace_back(temp);
                }
            }
        }
        return ans;
    }
```

## Approach 2

``` C++
    vector<int> sequentialDigits(int low, int high) {
        std::vector<int> ans;

        for (int i = 1; i <= 9; i++)
        {
            int curr = i;
            int next = i + 1;
            while (curr <= high && next <= 9)
            {
                curr = curr * 10 + next;
                if (curr >= low && curr <= high)
                {
                    ans.emplace_back(curr);
                }
                next++;
            }
        }
        std::sort(ans.begin(), ans.end());
        return ans;
    }
```

## Approach 3

``` C++
    vector<int> sequentialDigits(int low, int high) {
        std::string s = "123456789";
        std::vector<int> ans;

        for (int l = 0; l < 9; l++)
        {
            for (int r = l + 1; r <= 9; r++)
            {
                int curr = std::stoi(s.substr(l, r - l));
                if (curr > high)
                {
                    break;
                }
                if (curr >= low)
                {
                    ans.emplace_back(curr);
                }
            }
        }
        std::sort(ans.begin(), ans.end());
        return ans;
    }
```

