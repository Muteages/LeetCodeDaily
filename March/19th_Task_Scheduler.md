# Task Scheduler

https://leetcode.com/problems/task-scheduler

You are given an array of CPU tasks, each represented by letters A to Z, and a cooling time, n. Each cycle or interval allows the completion of one task. Tasks can be completed in any order, but there's a constraint: identical tasks must be separated by at least n intervals due to cooling time.

​Return the minimum number of intervals required to complete all tasks.

## Approach 1

``` C++
    int leastInterval(vector<char>& tasks, int cooling) {
        int n = tasks.size();
        if (cooling == 0)
        {
            return n;
        }

        std::vector<int> freq(26, 0);
        for (const char task : tasks)
        {
            freq[task - 'A']++;
        }
        std::sort(freq.rbegin(), freq.rend());
        int cycles = freq[0] - 1;
        int idels = cycles * cooling;
        for (int i = 1; i < 26; i++)
        {
            idels -= std::min(cycles, freq[i]);
        } 
        
        return idels < 0 ? n : n + idels;
    }
```

## Approach 2

``` C++
    int leastInterval(vector<char>& tasks, int cooling) {
        int n = tasks.size();
        if (0 == cooling)
        {
            return n;
        }

        std::vector<int> freq(26, 0);
        int maxFreq = 0;
        int maxFreqCnt = 0;
        for (const char task : tasks)
        {
            int currFreq = ++freq[task - 'A'];
            if (currFreq > maxFreq)
            {
                maxFreq = currFreq;
                maxFreqCnt = 1;
            }
            else if (currFreq == maxFreq)
            {
                maxFreqCnt++;
            }
        }

        return std::max(n, (maxFreq - 1) * (cooling + 1) + maxFreqCnt);
    }
```

## Approach 3

``` C++
    int leastInterval(vector<char>& tasks, int cooling) {
        int n = tasks.size();
        if (0 == cooling)
        {
            return n;
        }
        std::vector<int> freq(26, 0);
        for (const char task : tasks)
        {
            freq[task - 'A']++;
        }
        
        std::priority_queue<int> pq;
        for (int f : freq)
        {
            if (f != 0)
            {
                pq.emplace(f);
            }
        }
        int intervals = 0;
        while (pq.top() > 1)
        {
            std::vector<int> temp{};
            int currInterval = -1;
            while (!pq.empty() && currInterval != cooling)
            {
                currInterval++;
                int curFreq = pq.top();
                pq.pop();
                if (curFreq > 1)
                {
                    temp.emplace_back(curFreq - 1);
                }
            }
            intervals += std::max(currInterval, cooling + 1);

            for (int f : temp)
            {
                pq.emplace(f);
            }
        }

        return intervals + pq.size();
    }
```