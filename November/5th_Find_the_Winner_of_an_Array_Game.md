# Find the Winner of an Array Game

https://leetcode.com/problems/find-the-winner-of-an-array-game

Given an integer array arr of distinct integers and an integer k.

A game will be played between the first two elements of the array (i.e. arr[0] and arr[1]). In each round of the game, we compare arr[0] with arr[1], the larger integer wins and remains at position 0, and the smaller integer moves to the end of the array. The game ends when an integer wins k consecutive rounds.

Return the integer which will win the game.

## Approach 

``` C++
    int getWinner(vector<int>& arr, int k) {
        // Initialise
        int winner = arr[0]; 
        std::deque<int> candidates;
        for (int i = 1; i < arr.size(); i++)
        {
            candidates.emplace_back(arr[i]);
        }

        int streak = 0;
        while (streak < k)
        {
            int candidate = candidates.front();
            candidates.pop_front();

            if (winner >= candidate)
            { // Win
                streak++;
                candidates.emplace_back(candidate);
            }
            else
            { // Lose, reset
                streak = 1;
                candidates.emplace_back(winner);
                winner = candidate;
            }

            if (streak > arr.size() - 1)
            { // Avoid TLE
                break;
            }
        }
        return winner;
    }
```

## Approach 2

Improved solution

``` C++
    int getWinner(vector<int>& arr, int k) {
        // Initialise 
        int winner = arr[0];
        int streak = 0;
        for (int i = 1; i < arr.size(); i++)
        {
            if (winner >= arr[i])
            { // Win
                streak++;
            }
            else
            { // Lose, reset
                winner = arr[i];
                streak = 1;
            }
            
            if (streak == k)
            {
                return winner;
            }
        }
        return winner;
    }
```