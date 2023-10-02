# Remove Colored Pieces if Both Neighbors are the Same Color

https://leetcode.com/problems/remove-colored-pieces-if-both-neighbors-are-the-same-color/description

There are n pieces arranged in a line, and each piece is colored either by 'A' or by 'B'. You are given a string colors of length n where colors[i] is the color of the ith piece.

Alice and Bob are playing a game where they take alternating turns removing pieces from the line. In this game, Alice moves first.

Alice is only allowed to remove a piece colored 'A' if both its neighbors are also colored 'A'. She is not allowed to remove pieces that are colored 'B'.
Bob is only allowed to remove a piece colored 'B' if both its neighbors are also colored 'B'. He is not allowed to remove pieces that are colored 'A'.
Alice and Bob cannot remove pieces from the edge of the line.
If a player cannot make a move on their turn, that player loses and the other player wins.
Assuming Alice and Bob play optimally, return true if Alice wins, or return false if Bob wins.

## Approach 

TLE for some large cases:

``` C++
   bool winnerOfGame(string colors) {
        if (colors.length() < 3)
        {
            return false;
        }

        bool alice = true;
        while (true)
        {
            if (alice)
            {
                size_t pos = colors.find("AAA");
                if (pos != std::string::npos)
                {
                    colors.erase(pos + 1, 1);
                    alice = false;
                }
                else 
                {
                    return false;
                }
            }
            else
            {
                size_t pos = colors.find("BBB");
                if (pos != std::string::npos)
                {
                    colors.erase(pos + 1, 1);
                    alice = true;
                }
                else
                {
                    return true;
                }
            }
        }
        return false;
    }
```

## Approach 2
``` C++
    bool winnerOfGame(string colors) {
        if (colors.length() < 3)
        {
            return false;
        }

        int aliceCnt = 0;
        int bobCnt = 0;

        size_t pos = 0;
        while (pos < colors.length())
        {
            std::string temp = "";
            int len = 0;
            while (pos < colors.length() && colors[pos] == 'A')
            { 
                temp += colors[pos];
                pos++;
            }
            len = std::max(0, temp.length() - 2);
            aliceCnt += len;

            temp = ""; // reset
            while (pos < colors.length() && colors[pos] == 'B')
            {
                temp += colors[pos];
                pos++;
            }
            len = std::max(0, temp.length() - 2);
            bobCnt += len;
        }
        return aliceCnt > bobCnt;
    }
```

## Approach 3
``` C++
    bool winnerOfGame(string colors) {
        if (colors.length() < 3)
        {
            return false;
        }

        int aliceCnt = 0;
        int bobCnt = 0;

        for (size_t i = 1; i < colors.length() - 1; i++)
        {
            std::string temp = colors.substr(i - 1, 3);
            // 
            if (temp == "AAA")
            {
                aliceCnt++;
            }
            else if (temp == "BBB")
            {
                bobCnt++;
            }
        }

        /*  Avoid using string, faster
        for (size_t i = 1; i < colors.length() - 1; i++)
        {
            if (colors[i - 1] == colors[i] && colors[i] == colors[i + 1])
            {
                if (colors[i] == 'A')
                {
                    aliceCnt++;
                }
                else
                {
                    bobCnt++;
                }
            }
        }
        */

        return aliceCnt > bobCnt;
    }
```