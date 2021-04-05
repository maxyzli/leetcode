# Minimum Path Sum

## Solution 1

DFS (Time Limit Exceeded)

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

DP

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
