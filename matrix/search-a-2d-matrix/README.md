# Search a 2D Matrix

## Solution 1

Matrix

```java
/**
 * Question   : Search a 2D Matrix
 * Complexity : Time: O(m+n) ; Space: O(1)
 * Topics     : Matrix
 */
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int ROW_SIZE = matrix.length, COL_SIZE = matrix[0].length;

        int row = 0, col = COL_SIZE - 1;

        while (row < ROW_SIZE && col >= 0) {
            if (matrix[row][col] == target) return true;
            if (matrix[row][col] > target) {
                col--;
            } else if (matrix[row][col] < target) {
                row++;
            }
        }

        return false;
    }
}
```

## Solution 2

Binary Search

```java
/**
 * Question   : Search a 2D Matrix
 * Complexity : Time: O(log(m*n)) ; Space: O(1)
 * Topics     : Matrix
 */
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int m = matrix.length, n = matrix[0].length;

        int low = 0, high = m * n - 1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            int row = mid / n, col = mid % n;

            if (matrix[row][col] == target) {
                return true;
            } else if (matrix[row][col] > target) {
                high = mid - 1;
            } else {
                low = mid + 1;
            }
        }

        return false;
    }
}
```
