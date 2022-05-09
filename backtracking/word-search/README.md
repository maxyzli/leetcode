# Word Search

## Solution 1

Backtracking

```java
/**
 * Question   : 79. Word Search
 * Complexity : Time: O(m*n*3^k) ; Space: O(k)
 * Topics     : Backtracking
 */
class Solution {
    private int[][] directions = new int[][]{{-1, 0}, {0, 1}, {1, 0}, {0, -1}};

    public boolean exist(char[][] board, String word) {
        if (word == null || word.length() == 0) {
            return false;
        }

        for (int row = 0; row < board.length; row++) {
            for (int col = 0; col < board[0].length; col++) {
                if (board[row][col] == word.charAt(0)) {
                    if (dfs(board, word, 0, row, col)) {
                        return true;
                    }
                }
            }
        }

        return false;
    }

    private boolean dfs(char[][] board, String word, int idx, int row, int col) {
        if (row < 0 || row >= board.length || col < 0 || col >= board[0].length) {
            return false;
        }

        if (board[row][col] != word.charAt(idx)) {
            return false;
        }
        if (idx == word.length() - 1) {
            return true;
        }

        char origin = board[row][col];
        board[row][col] = '.';

        for (int[] direction : directions) {
            if (dfs(board, word, idx + 1, row + direction[0], col + direction[1])) {
                return true;
            }
        }

        board[row][col] = origin;

        return false;
    }
}
```
