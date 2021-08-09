# Island Perimeter

## Solution 1

DFS

```java
/**
 * Question   : 463. Island Perimeter
 * Complexity : Time: O(m*n) ; Space: O(m+n)
 * Topics     : DFS
 */
class Solution {
    private int[][] dirs = new int[][]{{-1, 0}, {0, 1}, {1, 0}, {0, -1}};
    
    public int islandPerimeter(int[][] grid) {
        if (grid == null || grid.length == 0) {
            return 0;
        }
        
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (grid[i][j] == 1) {
                    return dfs(grid, i, j);
                }
            }
        }
        
        return 0;
    }
    
    private int dfs(int[][] grid, int i, int j) {
        // borders
        if (!inArea(grid, i, j) || grid[i][j] == 0) {
            return 1;
        }
        // visited
        if (grid[i][j] == -1) {
            return 0;
        }
        
        // mark visited.
        grid[i][j] = -1;
        
        int perimeter = 0;
        for (int[] dir : dirs) {            
            int newRow = i + dir[0];
            int newCol = j + dir[1];
            perimeter += dfs(grid, newRow, newCol);
        }
        
        return perimeter;
    }
    
    private boolean inArea(int[][] grid, int i, int j) {
        return i >= 0 && j >= 0 && i < grid.length && j < grid[0].length;
    }
}
```
