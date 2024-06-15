# IPO

https://leetcode.com/problems/ipo

Suppose LeetCode will start its IPO soon. In order to sell a good price of its shares to Venture Capital, LeetCode would like to work on some projects to increase its capital before the IPO. Since it has limited resources, it can only finish at most k distinct projects before the IPO. Help LeetCode design the best way to maximize its total capital after finishing at most k distinct projects.

You are given n projects where the ith project has a pure profit profits[i] and a minimum capital of capital[i] is needed to start it.

Initially, you have w capital. When you finish a project, you will obtain its pure profit and the profit will be added to your total capital.

Pick a list of at most k distinct projects from given projects to maximize your final capital, and return the final maximized capital.

The answer is guaranteed to fit in a 32-bit signed integer.


## Approach 

``` C++
    int findMaximizedCapital(int k, int w, vector<int>& profits, vector<int>& capital) {
        const int n = profits.size();
        std::vector<std::pair<int, int>> c2p(n);  // capital - profit
        for (int i = 0; i < n; ++i) 
        {
            c2p[i] = {capital[i], profits[i]};
        }

        std::sort(c2p.begin(), c2p.end());
        std::priority_queue<int> maxProfits;
        int curr = 0;
        while(k--)
        {
            while (curr < n && c2p[curr].first <= w)
            { // Select all possible projects first
                maxProfits.emplace(c2p[curr].second);
                curr++;
            }

            if (!maxProfits.empty())
            { // Select the project with maximum profit
                w += maxProfits.top();
                maxProfits.pop();
            }
            else
            { // Don't have enough capital.
                break;
            }

        }
        return w;
    }
```