# N-Queens

## Solution 1

```java
/**
 * Question   : 51. N-Queens
 * Complexity : Time: O(n!) ; Space: O(n^2)
 * Topics     : Backtracking
 */
public class Solution {
    public List<List<String>> solveNQueens(int n) {
        if (n <= 0) {
            return new ArrayList<>();
        }

        char[][] board = new char[n][n];
        for (int i = 0; i < n; i++) {
            Arrays.fill(board[i], '.');
        }

        int col = 0;
        List<List<String>> res = new ArrayList<>();

        solveNQueensUtil(board, col, res);

        return res;
    }

    private void solveNQueensUtil(char[][] board, int col, List<List<String>> res) {
        // Column goes to the end, add to solution.
        if (col == board[0].length) {
            res.add(boardToList(board));
            return;
        }

        for (int row = 0; row < board.length; row++) {
            if (isValid(board, row, col)) {
                board[row][col] = 'Q';
                solveNQueensUtil(board, col + 1, res);
                board[row][col] = '.';
            }
        }
    }

    private List<String> boardToList(char[][] board) {
        List<String> list = new ArrayList<>();
        for (int i = 0; i < board.length; i++) {
            list.add(String.valueOf(board[i]));
        }
        return list;
    }

    private boolean isValid(char[][] board, int row, int col) {
        // Check the same row.
        for (int j = 0; j < board[0].length; j++) {
            if (board[row][j] != '.') {
                return false;
            }
        }

        // Check the same column.
        for (int i = 0; i < board.length; i++) {
            if (board[i][col] != '.') {
                return false;
            }
        }

        int i = row;
        int j = col;
        // Up left
        while (i >= 0 && j >= 0) {
            if (board[i][j] != '.') {
                return false;
            }
            i--;
            j--;
        }

        i = row;
        j = col;
        // Down left.
        while (i < board.length && j >= 0) {
            if (board[i][j] != '.') {
                return false;
            }
            i++;
            j--;
        }

        // Note:
        // We don't need to check the right part, because start from the left.
        // Right part is always empty.

        return true;
    }
}
```
