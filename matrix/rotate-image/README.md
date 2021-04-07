# Rotate Image

## Solution 1

Transpose and reverse row by row

```java
/**
 * Question   : 48. Rotate Image
 * Complexity : Time: O(m*n) ; Space: O(1)
 * Topics     : matrix
 */
class Solution {
    public void rotate(int[][] matrix) {
        int m = matrix.length;
        int n = matrix[0].length;

        // 1. Transpose
        for (int i = 0; i < m; i++) {
            for (int j = i; j < n; j++) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }

        // 2. Reverse row by row.
        for (int rowIdx = 0; rowIdx < m; rowIdx++) {
            int leftIdx = 0;
            int rightIdx = matrix[rowIdx].length - 1;

            while (leftIdx <= rightIdx) {
                int temp = matrix[rowIdx][leftIdx];
                matrix[rowIdx][leftIdx] = matrix[rowIdx][rightIdx];
                matrix[rowIdx][rightIdx] = temp;
                leftIdx++;
                rightIdx--;
            }
        }
    }
}
```
