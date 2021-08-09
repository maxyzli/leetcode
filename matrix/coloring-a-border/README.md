# Coloring A Border

## Solution 1

DFS

```java
/**
 * Question   : 1034. Coloring A Border
 * Complexity : Time: O(m*n) ; Space: O(m*n)
 * Topics     : Matrix
 */
class Solution {
    private int currColor;
    private int[][] dirs = new int[][]{{-1, 0}, {0, 1}, {1, 0}, {0, -1}};
    private boolean[][] visited;
    
    public int[][] colorBorder(int[][] grid, int row, int col, int color) {
        if (grid == null || grid.length == 0) {
            return grid; 
        }
        
        visited = new boolean[grid.length][grid[0].length];
        currColor = grid[row][col];
        
        if (currColor == color) {
            return grid;
        }
        
        dfs(grid, row, col, color);
        
        return grid;
    }
    
    private void dfs(int[][] grid, int row, int col, int color) {
       if (!inArea(grid, row, col) || grid[row][col] != currColor || visited[row][col]) {
           return;
       }
        
       visited[row][col] = true;

      // Check if current component is a border.
      for (int[] dir : dirs) {
           int nextRow = row + dir[0];
           int nextCol = col + dir[1];
           if (!inArea(grid, nextRow, nextCol) || (grid[nextRow][nextCol] != currColor && !visited[nextRow][nextCol])) {
                grid[row][col] = color;
           }
           dfs(grid, nextRow, nextCol, color);
       }
    }
    
    private boolean inArea(int[][] grid, int row, int col) {
        return row >= 0 && col >= 0 && row < grid.length && col < grid[0].length;
    }
}
```
