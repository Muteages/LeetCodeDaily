# Remove Duplicate Letters

https://leetcode.com/problems/remove-duplicate-letters

Given a string s, remove duplicate letters so that every letter appears once and only once. You must make sure your result is 
the smallest in lexicographical order
 among all possible results.

 ## Approach 
 ``` C++
     string removeDuplicateLetters(string s) {
        if (s.length() == 1)
        {
            return s;
        }
        std::vector<int> freq(26, 0);
        std::vector<int> visited(26, 0);
        for (auto& ch : s)
        {
            freq[ch - 'a']++;
        }

        std::string ans;
        for (auto& ch : s)
        {
            int curr = ch - 'a';
            freq[curr]--;

            if (!visited[curr])
            {
                while (!ans.empty() && ans.back() > ch && freq[ans.back() - 'a'] > 0)
                { // If the character int ans is not the smallest at the current bit, reset its status to unvisited and pop it.
                    visited[ans.back() - 'a'] = 0;
                    ans.pop_back();
                }

                ans += ch;
                visited[curr] = 1;
            }
        }

        return ans;
    }   
 ```