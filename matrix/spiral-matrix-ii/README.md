# Spiral Matrix II

## Solution 1

```java
/**
 * Question   : 59. Spiral Matrix II
 * Complexity : Time: O(m*n) ; Space: O(1)
 * Topics     : Array, Matrix
 */
class Solution {
    public int[][] generateMatrix(int n) {
        int[][] matrix = new int[n][n];

        int rowStart = 0;
        int rowEnd = n - 1;
        int colStart = 0;
        int colEnd = n - 1;

        int number = 1;

        while (rowStart <= rowEnd && colStart <= colEnd) {
            for (int j = colStart; j <= colEnd; j++) {
                matrix[rowStart][j] = number++;
            }

            rowStart++;

            for (int i = rowStart; i <= rowEnd; i++) {
                matrix[i][colEnd] = number++;
            }

            colEnd--;

            if (rowStart > rowEnd || colStart > colEnd) {
                return matrix;
            }

            for (int j = colEnd; j >= colStart; j--) {
                matrix[rowEnd][j] = number++;
            }

            rowEnd--;

            for (int i = rowEnd; i >= rowStart; i--) {
                matrix[i][colStart] = number++;
            }

            colStart++;
        }

        return matrix;
    }
}
```
