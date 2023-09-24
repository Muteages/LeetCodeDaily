# Champagne Tower

https://leetcode.com/problems/champagne-tower/description

We stack glasses in a pyramid, where the first row has 1 glass, the second row has 2 glasses, and so on until the 100th row.  Each glass holds one cup of champagne.

Then, some champagne is poured into the first glass at the top.  When the topmost glass is full, any excess liquid poured will fall equally to the glass immediately to the left and right of it.  When those glasses become full, any excess champagne will fall equally to the left and right of those glasses, and so on.  (A glass at the bottom row has its excess champagne fall on the floor.)


## Approach 1

1D DP
``` C++
    double champagneTower(int poured, int query_row, int query_glass) {
        std::vector<double> currentRow(1, poured);

        for (int row = 0; row < query_row; row++)
        {
            std::vector<double> nextRow(row + 2, 0.0); // Since it's 0-indexed, plus 2 here

            for (int i = 0; i < currentRow.size(); i++)
            {
                double excess = currentRow[i] - 1.0; // If the current glass is full, calculate the excess champagne
                if (excess > 0.0)
                {
                    nextRow[i] += excess * 0.5;
                    nextRow[i + 1] += excess * 0.5;
                }
            }

            // Update
            currentRow = nextRow;
        }

        return std::min(1.0, currentRow[query_glass]); // Maximum 1.0
    }
```

## Approach 2

2D PD

``` C++
    double champagneTower(int poured, int query_row, int query_glass) {
        std::vector<std::vector<double>> rows(query_row + 1, std::vector<double>(query_row + 1, 0.0));
        rows[0][0] = poured;

        for (int row = 0; row < query_row; row++)
        {
            for (int i = 0; i <= row; i++)
            {
                double excess = rows[row][i] - 1;
                if (excess > 0.0)
                {
                    rows[row + 1][i] += excess * 0.5;
                    rows[row + 1][i + 1] += excess * 0.5;
                }
            }
        }

        return std::min(1.0, rows[query_row][query_glass]);
    }
```