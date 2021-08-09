# Surrounded Regions

## Solution 1

```java
/**
 * Question   : 130. Surrounded Regions
 * Complexity : Time: O(m*n) ; Space: O(m+n)
 * Topics     : DP
 */
class Solution {
    private int[][] dirs = new int[][]{{-1, 0}, {0, 1}, {1, 0}, {0, -1}};
    
    public void solve(char[][] board) {
        if (board == null || board.length == 0) {
            return;
        }
        
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                if (board[i][j] == 'O' && (i == 0 || i == board.length - 1 || j == 0 || j == board[0].length - 1)) {
                    dfs(board, i, j);
                }
            }
        }
        
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                if (board[i][j] == 'O') {
                    board[i][j] = 'X';
                }
                if (board[i][j] == '#') {
                    board[i][j] = 'O';
                }
            }
        }
    }
    
    private void dfs(char[][] board, int i, int j) {
        if (i < 0 || j < 0 || i >= board.length || j >= board[0].length || board[i][j] == '#' || board[i][j] == 'X') {
            return;
        }
        
        board[i][j] = '#';
        
        for (int[] dir : dirs) {
            dfs(board, i + dir[0], j + dir[1]);
        }
    }
}
```
