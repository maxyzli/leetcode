# Flood Fill

## Solution 1

DFS

```java
/**
 * Question   : 733. Flood Fill
 * Complexity : Time: O(m*n) ; Space: O(m*n)
 * Topics     : DFS
 */
class Solution {
    private boolean[][] visited;
    private final int[][] directions = new int[][]{{-1, 0}, {0, 1}, {1, 0}, {0, -1}};

    public int[][] floodFill(int[][] image, int sr, int sc, int newColor) {
        if (image == null || image.length == 0) {
            return image;
        }

        int rows = image.length;
        int cols = image[0].length;

        int originColor = image[sr][sc];
        visited = new boolean[rows][cols];

        dfs(image, sr, sc, originColor, newColor);

        return image;
    }

    private void dfs(int[][] image, int i, int j, int originColor, int newColor) {
        if (i < 0 || j < 0 || i >= image.length || j >= image[0].length || visited[i][j]) {
            return;
        }


        if (image[i][j] == originColor) {
            image[i][j] = newColor;
            visited[i][j] = true;
            for (int[] direction : directions) {
                dfs(image, i + direction[0], j + direction[1], originColor, newColor);
            }
        }
    }
}
```
