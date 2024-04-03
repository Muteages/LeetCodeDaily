# Word Search

https://leetcode.com/problems/word-search

Given an m x n grid of characters board and a string word, return true if word exists in the grid.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

## Approach

``` C++
    int m{}, n{}, l{};
    bool backtracking(vector<vector<char>>& board, const std::string& word, int row, int col, int idx)
    {
        if (row < 0 || row == m || col < 0 || col == n || board[row][col] != word[idx])
        {
            return false;
        }
        if (idx == l - 1)
        { // Match all characters
            return true;
        }
        char temp = board[row][col]; // Store for replace later
        board[row][col] = '-1'; // Set as visited
        bool up    =  backtracking(board, word, row - 1, col, idx + 1);
        bool down  =  backtracking(board, word, row + 1, col, idx + 1);
        bool left  =  backtracking(board, word, row, col - 1, idx + 1);
        bool right =  backtracking(board, word, row, col + 1, idx + 1);
        board[row][col] = temp;
        return up || down || left || right;
    }

    bool exist(vector<vector<char>>& board, string word) {
        m = board.size();
        n = board[0].size();
        l = word.length();

        // To extract impossible cases, doing extra check
        if (m * n < l)
        {
            return false;
        }
        std::unordered_map<char, int> freq;
        for (const auto& b : board)
        {
            for (const auto& ch : b)
            {
                freq[ch]++;
            }
        }
        for (const char& ch : word)
        {
            freq[ch]--;
            if (freq[ch] < 0)
            {
                return false;
            }
        }
        for (int row = 0; row < m; row++)
        {
            for (int col = 0; col < n; col++)
            {
                if (backtracking(board, word, row, col, 0))
                {
                    return true;
                }
            }
        }
        return false;
    }
```

