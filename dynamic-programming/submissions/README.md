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

        int[][] dp = new int[m][n];

        int maxSquareLen = 0;

        for (int row = 0; row < m; row++) {
            for (int col = 0; col < n; col++) {
                if (matrix[row][col] == '1') {
                    if (row == 0 || col == 0) {
                        dp[row][col] = 1;
                    } else {
                        dp[row][col] = 1 + Math.min(Math.min(dp[row - 1][col], dp[row][col - 1]), dp[row - 1][col - 1]);
                    }
                    maxSquareLen = Math.max(maxSquareLen, dp[row][col]);
                }
            }
        }

        return maxSquareLen * maxSquareLen;
    }
}
```
