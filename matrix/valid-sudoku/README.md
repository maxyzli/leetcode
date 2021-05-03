# Valid Sudoku

## Solution 1

```java
/**
 * Question   : 36. Valid Sudoku
 * Complexity : Time: O(m*n) ; Space: O(1)
 * Topics     : Array, Matrix
 */
class Solution {
    public boolean isValidSudoku(char[][] board) {
        if (board == null || board.length == 0) {
            return false;
        }

        int n = board.length;

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (board[i][j] != '.' && !isValid(board, i, j)) {
                   return false;
                }
            }
        }

        return true;
    }

    private boolean isValid(char[][] board, int row, int col) {
        char val = board[row][col];

        board[row][col] = '.';

        for (int i = 0; i < board.length; i++) {
            if (board[i][col] == val) {
                return false;
            }
        }

        for (int j = 0; j < board.length; j++) {
            if (board[row][j] == val) {
                return false;
            }
        }

        int rowStart = (row / 3) * 3;
        int colStart = (col / 3) * 3;

        for (int i = rowStart; i < rowStart + 3; i++) {
            for (int j = colStart; j < colStart + 3; j++) {
                if (board[i][j] == val) {
                    return false;
                }
            }
        }

        board[row][col] = val;

        return true;
    }
}
```
