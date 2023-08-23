# Reorgnaize String

https://leetcode.com/problems/reorganize-string/description/

Given a string s, rearrange the characters of s so that any two adjacent characters are not the same.

Return any possible rearrangement of s or return "" if not possible.


## Approach 1 

Always use the two most frequent characters to build the string to avoid any two adjacent character are not the same.

``` C++
   string reorganizeString(string s) {
        std::unordered_map<char, int> freq;  // char - frequency
        for (const char& c : s)
        {
            freq[c]++;
        }

        std::priority_queue<std::pair<int, char>> sortedFreq; // max heap

        for (const auto& [c, f] : freq)
        {
            sortedFreq.emplace(f, c);
        }

        {
            auto [f, c] = sortedFreq.top();
            if (f > (s.length() + 1) / 2)
            { // if the highest frequency greater than the half of the string's length, fail the goal
                return "";
            }
        }

        std::string ans;

        while (sortedFreq.size() >= 2)
        { // Check two characters which have the first and second frequency each loop
            auto [f1, c1] = sortedFreq.top();
            sortedFreq.pop();
            ans += c1;
            f1--;

            auto [f2, c2] = sortedFreq.top();
            sortedFreq.pop();
            ans += c2;
            f2--;

            // Push the character back into the heap if it still exists
            if (f1 > 0)
            {
                sortedFreq.emplace(f1, c1);
            }
            if (f2 > 0)
            {
                sortedFreq.emplace(f2, c2);
            }
        }

        if (!sortedFreq.empty())
        {
            auto [f, c] = sortedFreq.top();
            if (f > 1)
            { // which means there must be two adjacent characters that are the same
                return "";
            }
            else 
            {
                ans += c;
            }
        }

        return ans;
    }
```

## Approach 2

Reserve the slots and insert the character into the proper position one by one. 

``` C++
    string reorganizeString(string s) {
        std::unordered_map<char, int> freq;  // char - frequency
        for (const char& c : s)
        {
            freq[c]++;
        }
        
        std::vector<char> sortedCh;
        for (const auto& [ch, f] : freq)
        {
            sortedCh.emplace_back(ch);
        }

        // sorted characters following their frequencies
        std::sort(sortedCh.begin(), sortedCh.end(), 
        [&](const char& c1, const char& c2){
            return freq[c1] > freq[c2];
        });

        if (freq[sortedCh[0]] > (s.length() + 1) / 2)
        { // The same as the first approach 
            return "";
        }
        std::string ans(s.length(), ' ');
        int i = 0;
        // insert the same characters to their positions one by one    0, 2, 4, 9...  and then 1, 3, 5, 7
        for (const auto& ch : sortedCh)
        {
            for (int j = 0; j < freq[ch]; j++)
            {
                if (i >= s.length())
                { // all even positions are occupied, swtich to odd positions
                    i = 1;
                }
                ans[i] = ch;
                i += 2;
            }
        }

        return ans;
    }
```