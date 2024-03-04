# Bag of Tokens

https://leetcode.com/problems/bag-of-tokens

You start with an initial power of power, an initial score of 0, and a bag of tokens given as an integer array tokens, where each tokens[i] donates the value of tokeni.

Your goal is to maximize the total score by strategically playing these tokens. In one move, you can play an unplayed token in one of the two ways (but not both for the same token):

Face-up: If your current power is at least tokens[i], you may play tokeni, losing tokens[i] power and gaining 1 score.
Face-down: If your current score is at least 1, you may play tokeni, gaining tokens[i] power and losing 1 score.
Return the maximum possible score you can achieve after playing any number of tokens.

## Approach 1

``` C++
    int bagOfTokensScore(vector<int>& tokens, int power) {
        if (tokens.empty())
        {
            return 0;
        }
        std::sort(tokens.begin(), tokens.end());
        if (power < tokens[0])
        {
            return 0;
        }
        int n = tokens.size();
        std::vector<int> sums(n);
        sums[0] = tokens[0];
        for (int i = 1; i < n; ++i)
        {
            sums[i] = sums[i - 1] + tokens[i];
        }
        int ans = 0;
        int maxRight = n - 1;
        for (int left = 0; left <= maxRight; left++)
        {
            int right = left;
            while (right <= maxRight && sums[right] <= power)
            {
                right++;
            }
            ans = std::max(right - left, ans);

            // Use one score to gain current maximum power 
            power += tokens[maxRight];
            maxRight--;
        }
        return ans;
    }
```

## Approach 2

``` C++
    int bagOfTokensScore(vector<int>& tokens, int power) {
        if (tokens.empty())
        {
            return 0;
        }        
        std::sort(tokens.begin(), tokens.end());
        int left = 0, right = tokens.size() - 1;
        int curScore = 0;

        while (left < right)
        {
            if (power >= tokens[left])
            {
                curScore++;
                power -= tokens[left++];
            }
            else if (curScore > 0)
            {
                curScore--;
                power += tokens[right--];
            }
            else
            {
                break;
            }
        }
        if (power >= tokens[left])
        {
            curScore++;
        }
        return curScore;
    }
```