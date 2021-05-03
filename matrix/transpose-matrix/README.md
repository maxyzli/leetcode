# Transpose Matrix

## Solution 1

```java
/**
 * Question   : 867. Transpose Matrix
 * Complexity : Time: O(m*n) ; Space: O(m*n)
 * Topics     : Array, Matrix
 */
class Solution {
    public int[][] transpose(int[][] matrix) {
        if (matrix == null || matrix.length == 0) {
            return matrix;
        }

        int m = matrix.length;
        int n = matrix[0].length;

        int[][] t = new int[n][m];

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                t[j][i] = matrix[i][j];
            }
        }

        return t;
    }
}
```
