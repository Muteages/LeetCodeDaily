# The K Weakest Rows in a Matrix

https://leetcode.com/problems/the-k-weakest-rows-in-a-matrix/description

You are given an m x n binary matrix mat of 1's (representing soldiers) and 0's (representing civilians). The soldiers are positioned in front of the civilians. That is, all the 1's will appear to the left of all the 0's in each row.

A row i is weaker than a row j if one of the following is true:

The number of soldiers in row i is less than the number of soldiers in row j.
Both rows have the same number of soldiers and i < j.
Return the indices of the k weakest rows in the matrix ordered from weakest to strongest.

## Approach 1

Use priority queue

``` C++
    vector<int> kWeakestRows(vector<vector<int>>& mat, int k) {
        int m = mat.size();
        int n = mat[0].size();

        std::priority_queue<std::pair<int, int>, std::vector<std::pair<int, int>>, std::greater<>> pq; // soldiers cnt - row idx
        for (int r = 0; r < m; r++)
        {   // Calculate the soldiers number of each row
            int soldiers = 0;
            for (int c = 0; c < n; c++)
            {
                if (mat[r][c] == 1)
                {
                    soldiers++;
                }
            }
            pq.emplace(soldiers, r);
        }

        std::vector<int> ans(k);
        for (int i = 0; i < k; i++)
        {
            if (!pq.empty())
            {
                ans[i] = pq.top().second;
                pq.pop();
            }
        }
        return ans;
    }
```

## Approach 2 

``` C++
    vector<int> kWeakestRows(vector<vector<int>>& mat, int k) {
        int m = mat.size();

        std::priority_queue<std::pair<int, int>> pq; // soldiers cnt - row idx
        for (int row = 0; row < k; row++)
        {   // Fill k row first
            int soldiers = std::accumulate(mat[row].begin(), mat[row].end(), 0);
            pq.emplace(soldiers, row);
        }

        for (int row = k; row < m; row++)
        {   // Replace the strongest rows
            int soldiers = std::accumulate(mat[row].begin(), mat[row].end(), 0);
            int currMax = pq.top().first;
            if (soldiers < currMax)
            {
                pq.emplace(soldiers, row);
                pq.pop();
            } 
        }

        std::vector<int> ans(k);
        for (int i = k - 1; i >= 0; i--)
        {
            ans[i] = pq.top().second;
            pq.pop();
        }
        return ans;
    }
```