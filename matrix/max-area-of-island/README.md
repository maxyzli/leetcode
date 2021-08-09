# Max Area of Island

## Solution 1

DFS

```java
/**
 * Question   : 695. Max Area of Island
 * Complexity : Time: O(m*n) ; Space: O(m+n)
 * Topics     : Matrix
 */
class Solution {
    int[][] dirs = new int[][]{{-1, 0}, {0, 1}, {1, 0}, {0, -1}};
    
    public int maxAreaOfIsland(int[][] grid) {
        if (grid == null || grid.length == 0) {
            return 0;
        }
       
        int maxArea = 0;
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (grid[i][j] == 1) {
                    maxArea = Math.max(maxArea, dfs(grid, i, j));
                }
            }  
        }
        
        return maxArea;
    }
    
    private int dfs(int[][] grid, int i, int j) {
        if (i < 0 || j < 0 || i >= grid.length || j >= grid[0].length || grid[i][j] == 0) {
            return 0;
        }
        
        grid[i][j] = 0;
        
        int area = 1;
        
        for (int[] dir : dirs) {
            area += dfs(grid, i + dir[0], j + dir[1]);
        }
        
        return area;
    }
}
```
