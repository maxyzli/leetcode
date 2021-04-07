# Search a 2D Matrix II

## Solution 1

```java
import java.util.*;

/**
 * Question   : 240. Search a 2D Matrix II
 * Complexity : Time: O(m+n) ; Space: O(1)
 * Topics     : Matrix
 */
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if (matrix == null || matrix.length == 0) {
            return false;
        }

        int row = 0;
        int col = matrix[0].length - 1;

        while (row < matrix.length && col >= 0) {
            if (matrix[row][col] == target) {
                return true;
            } else if (matrix[row][col] < target) {
                row++;
            } else {
                col--;
            }
        }

        return false;
    }
}
```
