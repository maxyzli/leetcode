# Maximal Rectangle

## Solution 1

DP + Hash Table

```java
/**
 * Question   : 85. Maximal Rectangle
 * Complexity : Time: O(m*n) ; Space: O(m*n)
 * Topics     : DP
 */
public class Solution {
    public int maximalRectangle(char[][] matrix) {
        if (matrix.length == 0) {
            return 0;
        }

        int m = matrix.length;
        int n = matrix[0].length;

        // dp[i] = the longest contiguous 1 start from index i.
        int[][] dp = new int[m][n];

        for (int i = 0; i < m; i++) {
            if (matrix[i][0] == '1') {
                dp[i][0] = 1;
            }
        }

        for (int i = 0; i < m; i++) {
            for (int j = 1; j < n; j++) {
                if (matrix[i][j] == '1') {
                    dp[i][j] = dp[i][j - 1] + 1;
                }
            }
        }

        int maximum = 0;

        // 84. Largest Rectangle in Histogram
        // For every column we try to find largest rectangle in there.
        for (int j = 0; j < n; j++) {
            Stack<Integer> stack = new Stack<>();
            int[] leftSmallerIdx = new int[m];
            int[] rightSmallerIdx = new int[m];

            for (int i = 0; i < m; i++) {
                while (!stack.isEmpty() && dp[stack.peek()][j] >= dp[i][j]) {
                    stack.pop();
                }
                leftSmallerIdx[i] = stack.isEmpty() ? -1 : stack.peek();
                stack.push(i);
            }
            stack.clear();
            for (int i = m - 1; i >= 0; i--) {
                while (!stack.isEmpty() && dp[stack.peek()][j] >= dp[i][j]) {
                    stack.pop();
                }
                rightSmallerIdx[i] = stack.isEmpty() ? m : stack.peek();
                stack.push(i);
            }

            for (int i = 0; i < m; i++) {
                int height = dp[i][j];
                int width = (rightSmallerIdx[i] - leftSmallerIdx[i] - 1);
                maximum = Math.max(maximum, height * width);
            }
        }

        return maximum;
    }
}
```
