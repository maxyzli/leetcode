# Spiral Matrix

## Solution 1

```java
/**
 * Question   : 54. Spiral Matrix
 * Complexity : Time: O(m*n) ; Space: O(1)
 * Topics     : matrix
 */
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        if (matrix == null) {
            return new LinkedList<>();
        }

        int m = matrix.length;
        int n = matrix[0].length;

        int rowMin = 0;
        int rowMax = matrix.length - 1;
        int colMin = 0;
        int colMax = matrix[0].length - 1;

        List<Integer> res = new LinkedList<>();

        while (rowMin <= rowMax && colMin <= colMax) {
            // Go left.
            for (int j = colMin; j <= colMax; j++) {
                res.add(matrix[rowMin][j]);
            }
            rowMin++;

            // Go down.
            for (int i = rowMin; i <= rowMax; i++) {
                res.add(matrix[i][colMax]);
            }
            colMax--;

            if (rowMin > rowMax || colMin > colMax) {
                return res;
            }

            // Go left.
            for (int j = colMax; j >= colMin; j--) {
                res.add(matrix[rowMax][j]);
            }
            rowMax--;

            // Go Up.
            for (int i = rowMax; i >= rowMin; i--) {
                res.add(matrix[i][colMin]);
            }
            colMin++;
        }

        return res;
    }
}
```
