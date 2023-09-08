# Text Justification

https://leetcode.com/problems/text-justification/description/

Given an array of strings words and a width maxWidth, format the text such that each line has exactly maxWidth characters and is fully (left and right) justified.

You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces ' ' when necessary so that each line has exactly maxWidth characters.

Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line does not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.

For the last line of text, it should be left-justified, and no extra space is inserted between words.


## Approach

``` C++
    vector<string> fullJustify(vector<string>& words, int maxWidth) {
        std::vector<std::string> ans;

        int totalWords = words.size();
        int curWord = 0;
        while (curWord < totalWords)
        {
            // Step 1: find the current line range
            std::string curString = words[curWord]; // Add the current word first
            int curWidth = curString.length();
            int nextWord = curWord + 1;
            while (nextWord < totalWords && curWidth + 1 + words[nextWord].length() <= maxWidth)
            {
                curWidth = curWidth + 1 + words[nextWord].length();  // Adding extra 1 means the space after each word
                nextWord++;
            } // Notice that after the loop, nextWord is not the real tail of current range. [curWord, nextWord)

            // Step 2: Handle the spaces
            int spaceNum = maxWidth - curWidth;// Spaces that need to be filled
            int wordNum = nextWord - curWord;  // Word number of the current line

            if (nextWord == totalWords || wordNum == 1)
            { // Two cases: only one word in this line or the last line, we can simply add all space after the word

                for (int i = curWord + 1; i < nextWord; i++)
                {  // Add all words
                    curString += ' ';  // The space after each word
                    curString += words[i];
                }

                // Spaces
                for (int i = 0; i < spaceNum; i++)
                {
                    curString += ' ';
                }
            }
            
            else
            { // Insert spaces
                int slotsNum = wordNum - 1;
                int spacesInEachSlot = spaceNum / slotsNum; // Space number in each slot
                int remainder = spaceNum % slotsNum; // Remaining spaces

                for (int i = curWord + 1; i < nextWord; i++)
                {
                    curString += ' ';  // "Default" space

                    for (int j = 0; j < spacesInEachSlot; j++)
                    { // Distribute spaces evenly
                        curString += ' ';
                    }

                    if (remainder > 0)
                    { // Assign remaining spaces from left to right
                        curString += ' ';
                        remainder--;
                    }
                    curString += words[i];
                }
            }

            ans.emplace_back(std::move(curString));
            curWord = nextWord;
        }

        return ans;
    }
```