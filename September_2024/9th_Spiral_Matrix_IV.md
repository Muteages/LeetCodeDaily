# Spiral Matrix IV

https://leetcode.com/problems/spiral-matrix-iv/

You are given two integers m and n, which represent the dimensions of a matrix.

You are also given the head of a linked list of integers.

Generate an m x n matrix that contains the integers in the linked list presented in spiral order (clockwise), starting from the top-left of the matrix. If there are remaining empty spaces, fill them with -1.

Return the generated matrix.


## Approach 
``` C++
    vector<vector<int>> spiralMatrix(int m, int n, ListNode* head) {
        std::vector<std::vector<int>> ans(m, std::vector<int>(n, -1));
        int rowS = 0;
        int rowL = m-1;
        int colS = 0;
        int colL = n-1;

        while(head)
        {
            // Right
            for(int i = colS; i <= colL && head; i++) {
                ans[rowS][i] = head->val;
                head = head->next;
            }
            rowS++;

            // Down
            for(int i = rowS ; i <= rowL && head; i++) {
                ans[i][colL] = head->val;
                head = head->next;
            }
            colL--;

            // Left
            for(int i = colL; i >= colS && head; i--) {
                ans[rowL][i] = head->val;
                head = head->next;
            }
            rowL--;

            // Up
            for(int i = rowL; i >= rowS && head; i--) {
                ans[i][colS] = head->val;
                head = head->next;
            }
            colS++;
        }
        return ans;
    }
```