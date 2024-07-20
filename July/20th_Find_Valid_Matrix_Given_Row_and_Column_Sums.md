# Find Valid Matrix Given Row and Column Sums

https://leetcode.com/problems/find-valid-matrix-given-row-and-column-sums

You are given two arrays rowSum and colSum of non-negative integers where rowSum[i] is the sum of the elements in the ith row and colSum[j] is the sum of the elements of the jth column of a 2D matrix. In other words, you do not know the elements of the matrix, but you do know the sums of each row and column.

Find any matrix of non-negative integers of size rowSum.length x colSum.length that satisfies the rowSum and colSum requirements.

Return a 2D array representing any matrix that fulfills the requirements. It's guaranteed that at least one matrix that fulfills the requirements exists.

## Approach 

``` C++
    vector<vector<int>> restoreMatrix(vector<int>& rowSum, vector<int>& colSum) {
        const int m = rowSum.size(), n = colSum.size();
        std::vector<std::vector<int>> mat(m, std::vector<int>(n, 0));
        int row = 0, col = 0;
        while (row < m && col < n)
        {
            int temp = std::min(rowSum[row], colSum[col]);
            mat[row][col] = temp;
            rowSum[row] -= temp;
            colSum[col] -= temp;
            row += (rowSum[row] == 0);
            col += (colSum[col] == 0);
        }
        return mat;
    }
```

``` JavaScript
var restoreMatrix = function(rowSum, colSum) {
    const m = rowSum.length, n = colSum.length;
    const mat = Array.from({length : m}, () => Array(n).fill(0));
    let row = 0, col = 0;
    while (row < m && col < n) {
        let temp = Math.min(rowSum[row], colSum[col]);
        mat[row][col] = temp;
        rowSum[row] -= temp;
        colSum[col] -= temp;
        row += (rowSum[row] === 0);
        col += (colSum[col] === 0);
    }
    return mat;
};
```

