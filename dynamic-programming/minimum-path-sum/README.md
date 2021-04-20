# Minimum Path Sum

## Solution 1

DFS (Time Limit Exceeded)

Calculate the result at calling phase.

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

## Solution 2

DFS (Time Limit Exceeded)

Calculate the result at returning phase.

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

## Solution 3

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

## Solution 4

Bottom-Up DP

`memo[i][j]`: represent the minimum path sum to destination.

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
        memo[m - 1][n - 1] = grid[m - 1][n - 1];

        // Initialization.
        for (int j = n - 2; j >= 0; j--) {
            memo[m - 1][j] += grid[m - 1][j] + memo[m - 1][j + 1];
        }
        for (int i = m - 2; i >= 0; i--) {
            memo[i][n - 1] += grid[i][n - 1] + memo[i + 1][n - 1];
        }

        for (int i = m - 2; i >= 0; i--) {
            for (int j = n - 2; j >= 0; j--) {
                memo[i][j] = grid[i][j] + Math.min(memo[i + 1][j], memo[i][j + 1]);
            }
        }

        return memo[0][0];
    }
}
```

## Solution 5

Bottom-Up DP

`memo[i][j]`: represent the minimum path sum to grid (i, j).

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

## Solution 6

Bottom-Up DP (State Compression)

`memo[i][j]`: represent the minimum path sum to grid (i, j).

```java
/**
 * Question   : 64. Minimum Path Sum
 * Topics     : DP
 * Complexity : Time: O(m+n) ; Space: O(n)
 */
class Solution {
    public int minPathSum(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;

        int[] memo = new int[n];
        memo[0] = grid[0][0];

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (i == 0 && j != 0) {
                    memo[j] = grid[i][j] + memo[j - 1];
                } else if (i != 0 && j == 0) {
                    memo[j] = grid[i][j] + memo[j];
                } else if (i != 0 && j != 0) {
                    memo[j] = grid[i][j] + Math.min(memo[j], memo[j - 1]);
                }
            }
        }

        return memo[n - 1];
    }
}
```
