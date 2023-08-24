# Excel Sheet Column Title

https://leetcode.com/problems/excel-sheet-column-title/description/

Given an integer columnNumber, return its corresponding column title as it appears in an Excel sheet.

## Approach 1

```
    string convertToTitle(int columnNumber) {
        std::string title;

        // 26 
        while (columnNumber > 0)
        {
            char curBit;
            if (curBit = (columnNumber % 26))
            {
                curBit = curBit - 1 + 'A';
            }
            else 
            {
                curBit = 'Z';
            }        
            title = curBit + title;
            columnNumber = (columnNumber - 1) / 26; 
        }
        return title;
    }
```

## Approach 2 

A little improve 

```
    string convertToTitle(int columnNumber) {
        std::string title;

        // 26 
        while (columnNumber > 0)
        {
            char curBit = (columnNumber - 1) % 26  + 'A';
            title = curBit + title;
            columnNumber = (columnNumber - 1) / 26;   // avoid the final 1
        }
        return title;
    }
```