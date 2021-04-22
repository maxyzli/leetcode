# Maximal Square

## Solution 1

```java
/**
 * Question   : Maximal Square
 * Topics     : DP
 * Complexity : Time: O(n^2) ; Space: O(n^2)
 */
class Solution {
    public int maximalSquare(char[][] matrix) {
        if (matrix == null || matrix.length == 0) {
            return 0;
        }

        int m = matrix.length;
        int n = matrix[0].length;

        int[][] memo = new int[m][n];

        int maxSquareLen = 0;

        for (int row = 0; row < m; row++) {
            for (int col = 0; col < n; col++) {
                if (matrix[row][col] == '1') {
                    if (row == 0 || col == 0) {
                        memo[row][col] = 1;
                    } else {
                        memo[row][col] = 1 + Math.min(Math.min(memo[row - 1][col], memo[row][col - 1]), memo[row - 1][col - 1]);
                    }
                    maxSquareLen = Math.max(maxSquareLen, memo[row][col]);
                }
            }
        }

        return maxSquareLen * maxSquareLen;
    }
}
```
