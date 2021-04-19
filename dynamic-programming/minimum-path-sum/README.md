# Minimum Path Sum

## Solution 1

DFS (Time Limit Exceeded)

Not recommended. Not thinking of a tree structure.

```java
/**
 * Question   : 64. Minimum Path Sum
 * Topics     : DP
 * Complexity : Time: O(exp) ; Space: O(m+n)
 */
class Solution {
    int min = Integer.MAX_VALUE;

    public int minPathSum(int[][] grid) {
        min = Integer.MAX_VALUE;
        dfs(grid, 0, 0, 0);
        return min;
    }

    private void dfs(int[][] grid, int row, int col, int sum) {
        if (row >= grid.length || col >= grid[0].length) {
            return;
        }

        sum += grid[row][col];

        if (row == grid.length - 1 && col == grid[0].length - 1) {
            min = Math.min(min, sum);
            return;
        }

        dfs(grid, row + 1, col, sum);
        dfs(grid, row, col + 1, sum);
    }
}
```

## Solution 2

DFS 2 (Time Limit Exceeded)

Get the result from the leaf.

```java
/**
 * Question   : 64. Minimum Path Sum
 * Topics     : DP
 * Complexity : Time: O(exp) ; Space: O(m+n)
 */
class Solution {
    private int min = Integer.MAX_VALUE;
    private final int[][] dirs = new int[][]{{1, 0}, {0, 1}};

    public int minPathSum(int[][] grid) {
        min = Integer.MAX_VALUE;
        dfs(grid, 0, 0, grid[0][0]);
        return min;
    }

    private void dfs(int[][] grid, int row, int col, int sum) {
        if (row == grid.length - 1 && col == grid[0].length - 1) {
            min = Math.min(min, sum);
            return;
        }

        // Think like a tree.
        for (int i = 0; i < dirs.length; i++) {
            int[] dir = dirs[i];
            int nextRow = row + dir[0];
            int nextCol = col + dir[1];
            if (nextRow < grid.length && nextCol < grid[0].length) {
                int nextSum = sum + grid[nextRow][nextCol];
                dfs(grid, nextRow, nextCol, nextSum);
            }
        }
    }
}
```

## Solution 3

DFS 2 (Time Limit Exceeded)

Get the result from the top.

```java
/**
 * Question   : 64. Minimum Path Sum
 * Topics     : DP
 * Complexity : Time: O(exp) ; Space: O(m+n)
 */
class Solution {
    private int min = Integer.MAX_VALUE;
    private final int[][] dirs = new int[][]{{1, 0}, {0, 1}};

    public int minPathSum(int[][] grid) {
        return dfs(grid, 0, 0);
    }

    private int dfs(int[][] grid, int row, int col) {
        if (row == grid.length - 1 && col == grid[0].length - 1) {
            return grid[row][col];
        }

        // Think like a tree.
        int min = Integer.MAX_VALUE;
        for (int i = 0; i < dirs.length; i++) {
            int[] dir = dirs[i];
            int nextRow = row + dir[0];
            int nextCol = col + dir[1];
            if (nextRow < grid.length && nextCol < grid[0].length) {
                int subMinPathSum = dfs(grid, nextRow, nextCol);
                min = Math.min(min, grid[row][col] + subMinPathSum);
            }
        }

        return min;
    }
}
```

## Solution 4

Top-Down DP

```java
 /**
 * Question   : 64. Minimum Path Sum
 * Topics     : DP
 * Complexity : Time: O(exp) ; Space: O(m+n)
 */
class Solution {
    private int min = Integer.MAX_VALUE;
    private final int[][] dirs = new int[][]{{1, 0}, {0, 1}};
    // Memorization.
    int[][] memo;

    public int minPathSum(int[][] grid) {
        memo = new int[grid.length][grid[0].length];
        return dfs(grid, 0, 0);
    }

    private int dfs(int[][] grid, int row, int col) {
        if (row == grid.length - 1 && col == grid[0].length - 1) {
            return grid[row][col];
        }

        if (memo[row][col] != 0) {
            return memo[row][col];
        }

        // Think like a tree.
        int min = Integer.MAX_VALUE;
        for (int i = 0; i < dirs.length; i++) {
            int[] dir = dirs[i];
            int nextRow = row + dir[0];
            int nextCol = col + dir[1];
            if (nextRow < grid.length && nextCol < grid[0].length) {
                int subMinPathSum = dfs(grid, nextRow, nextCol);
                min = Math.min(min, grid[row][col] + subMinPathSum);
            }
        }
        
        memo[row][col] = min;

        return memo[row][col];
    }
}
```

## Solution 5

Bottom-Up DP

```java
/**
 * Question   : 64. Minimum Path Sum
 * Topics     : DP
 * Complexity : Time: O(m+n) ; Space: O(m+n)
 */
class Solution {
    public int minPathSum(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;

        int[][] memo = new int[m][n];
        memo[0][0] = grid[0][0];

        // Calculate first column.
        for (int i = 1; i < m; i++) {
            memo[i][0] = memo[i - 1][0] + grid[i][0];
        }
        // Calculate first row.
        for (int j = 1; j < n; j++) {
            memo[0][j] = memo[0][j - 1] + grid[0][j];
        }

        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                memo[i][j] = grid[i][j] + Math.min(memo[i - 1][j], memo[i][j - 1]);
            }
        }

        return memo[m - 1][n - 1];
    }
}
```
