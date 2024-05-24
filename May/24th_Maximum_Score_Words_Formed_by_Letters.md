# Maximum Score Words Formed by Letters

https://leetcode.com/problems/maximum-score-words-formed-by-letters


Given a list of words, list of  single letters (might be repeating) and score of every character.

Return the maximum score of any valid set of words formed by using the given letters (words[i] cannot be used two or more times).


## Approach 

``` C++
    int ans, n;
    std::vector<int> wordScores;

    int maxScoreWords(vector<string>& words, vector<char>& letters, vector<int>& score) {
        ans = 0;
        n = words.size();
        std::vector<int> freq(26, 0); // Store frequencies of each letter
        for (char letter : letters)
        {
            freq[letter - 'a']++;
        }
        wordScores.resize(n, 0); // Store scores of each word
        for (int i = 0; i < n; i++)
        {
            for (char ch : words[i])
            {
                wordScores[i] += score[ch - 'a'];
            }
        }
        backtrack(words, freq, 0, 0);
        return ans;
    }

    void backtrack(std::vector<std::string>& words, std::vector<int>& freq, int idx, int curScore)
    {
        if (idx == n)
        {
            ans = std::max(ans, curScore);
            return;
        }
        std::vector<int> tempFreq = freq;
        int tempScore = curScore;

        // Skip current word
        backtrack(words, freq, idx + 1, curScore);

        std::string& word = words[idx];
        if (isValid(word, tempFreq, tempScore, idx))
        {
            backtrack(words, tempFreq, idx + 1, tempScore);
        }

    }

    bool isValid(const std::string& word, std::vector<int>& freq, int& curScore, int idx)
    {
        for (char ch : word)
        {
            if (--freq[ch - 'a'] < 0)
            {
                return false;
            }
        }
        curScore += wordScores[idx];
        return true;
    }
```