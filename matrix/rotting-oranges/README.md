# Rotting Oranges

## Solution 1

BFS

```java
/**
 * Question   : 994. Rotting Oranges
 * Complexity : Time: O(m*n) ; Space: O(m*n)
 * Topics     : Matrix, BFS
 */
class Solution {
    private int[][] dirs = new int[][]{{-1, 0}, {0, 1}, {1, 0}, {0, -1}};

    public int orangesRotting(int[][] grid) {
        if (grid == null || grid.length == 0) {
            return 0;
        }

        Queue<int[]> q = new ArrayDeque();

        int freshCount = 0;
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (grid[i][j] == 1) {
                    freshCount++;
                } else if (grid[i][j] == 2) {
                    q.offer(new int[]{i, j});
                }
            }
        }

        int minutes = 0;

        while (!q.isEmpty()) {
            boolean found = false;
            int size = q.size();

            for (int i = 0; i < size; i++) {
                int[] pos = q.poll();
                for (int[] dir : dirs) {
                    int nextRow = pos[0] + dir[0];
                    int nextCol = pos[1] + dir[1];
                    if (inArea(grid, nextRow, nextCol) && grid[nextRow][nextCol] == 1) {
                        freshCount--;
                        grid[nextRow][nextCol] = 2;
                        q.offer(new int[]{nextRow, nextCol});
                        found = true;
                    }
                }
            }

            if (found) {
                minutes++;
            }
        }

        if (freshCount != 0) {
            return -1;
        } else {
            return minutes;
        }
    }

    private boolean inArea(int[][] grid, int row, int col) {
        return row >= 0 && col >= 0 && row < grid.length && col < grid[0].length;
    }
}
```
