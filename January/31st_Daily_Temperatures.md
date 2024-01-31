# Daily Temperatures

https://leetcode.com/problems/daily-temperatures

Given an array of integers temperatures represents the daily temperatures, return an array answer such that answer[i] is the number of days you have to wait after the ith day to get a warmer temperature. If there is no future day for which this is possible, keep answer[i] == 0 instead.

## Approach 1

Brute force, TLE on large cases
``` C++
    vector<int> dailyTemperatures(vector<int>& temperatures) {
        int n = temperatures.size();
        std::vector<int> ans(n);
        for (int i = 0; i < n - 1; i++)
        {
            for (int j = i + 1; j < n; j++)
            {
                if (temperatures[j] > temperatures[i])
                {
                    ans[i] = j - i;
                    break;
                }
            }
        }
        return ans;
    }
```

## Approach 2

Utilise stack to track the next greater number of each element
``` C++
    vector<int> dailyTemperatures(vector<int>& temperatures) {
        int n = temperatures.size();
        std::vector<int> ans(n);
        std::stack<int> st;
        for (int i = 0; i < n; i++)
        {
            while (!st.empty() && temperatures[i] > temperatures[st.top()])
            { // Indicates that the current number is the next greater number of stack's top element
                ans[st.top()] = i - st.top();
                st.pop();
            }
            st.emplace(i);
        }
        return ans;
    }
```

