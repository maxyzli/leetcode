# Sudoku Solver

## Solution 1

```java
/**
 * Question   : 37. Sudoku Solver
 * Complexity : Time: O(9^n^2) ; Space: O(n^2)
 * Topics     : Backtracking
 */
class Solution {
    private final int MAX_NUM = 9;
    private final int BOX_SIZE = 3;

    public void solveSudoku(char[][] board) {
        int row = 0;
        int col = 0;
        solveSudokuUtil(board, row, col);
    }

    // We can the board column by column.
    private boolean solveSudokuUtil(char[][] board, int row, int col) {
        if (col == board[0].length) {
            return true;
        }
        // Row end -> go to next column.
        if (row == board.length) {
            return solveSudokuUtil(board, 0, col + 1);
        }
        // If there's a value already in the cell, move to next cell.
        if (board[row][col] != '.') {
            return solveSudokuUtil(board, row + 1, col);
        }

        for (int num = 1; num <= MAX_NUM; num++) {
            if (isValid(board, row, col, num)) {
                board[row][col] = (char) (num + '0');
                if (solveSudokuUtil(board, row + 1, col)) {
                    return true;
                }
                board[row][col] = '.';
            }
        }

        return false;
    }

    private boolean isValid(char[][] board, int row, int col, int num) {
        char numChar = (char) (num + '0');

        // Each of the digits 1-9 must occur exactly once in each row.
        for (int j = 0; j < board[0].length; j++) {
            if (board[row][j] == numChar) {
                return false;
            }
        }

        // Each of the digits 1-9 must occur exactly once in each column.
        for (int i = 0; i < board.length; i++) {
            if (board[i][col] == numChar) {
                return false;
            }
        }

        // Each of the digits 1-9 must occur exactly once in each of the 9 3x3 sub-boxes of the grid.
        int rowBegin = (row / BOX_SIZE) * BOX_SIZE;
        int colBegin = (col / BOX_SIZE) * BOX_SIZE;
        for (int i = rowBegin; i < rowBegin + BOX_SIZE; i++) {
            for (int j = colBegin; j < colBegin + BOX_SIZE; j++) {
                if (board[i][j] == numChar) {
                    return false;
                }
            }
        }

        return true;
    }
}
```
