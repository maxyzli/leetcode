# Minesweeper

## Solution 1

DFS

```java
class Solution {
    int[][] dirs = new int[][]{{-1, 0}, {0, 1}, {1, 0}, {0, -1}, {-1, -1}, {-1, 1}, {1, 1}, {1, -1}};
    
    public char[][] updateBoard(char[][] board, int[] click) {
        if (board == null || board.length == 0) {
            return board;
        }
        
        int row = click[0];
        int col = click[1];
        
        if (board[row][col] == 'M') {
            board[row][col] = 'X';
        } else if (board[row][col] == 'E') {
            dfs(board, row, col);
        }
        
        return board;
    }
    
    private void dfs(char[][] board, int i, int j) {
        if (!inArea(board, i, j) || board[i][j] != 'E') {
            return;
        }
       
        // Calculate the result for current block.
        int mineCount = 0;
        for (int[] dir : dirs) {
            int nextRow = i + dir[0];
            int nextCol = j + dir[1];
            if (inArea(board, nextRow, nextCol) && board[nextRow][nextCol] == 'M') {
                mineCount++;
            }
        }
        
        if (mineCount == 0) {
            board[i][j] = 'B';
            for (int[] dir : dirs) {
                 dfs(board, i + dir[0], j + dir[1]);
            }
        } else {
            board[i][j] = (char)(mineCount + '0');
        }
    }
    
    private boolean inArea(char[][] board, int i, int j) {
        return i >= 0 && j >= 0 && i < board.length && j < board[0].length;
    }
}
```
