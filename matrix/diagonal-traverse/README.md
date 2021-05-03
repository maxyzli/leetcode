# Diagonal Traverse

## Solution 1

```java
import java.util.*;

/**
 * Question   : 498. Diagonal Traverse
 * Complexity : Time: O(m*n) ; Space: O(1)
 * Topics     : Array, Matrix
 */
class Solution {
    public int[] findDiagonalOrder(int[][] mat) {
        if (mat == null || mat.length == 0) {
            return mat[0];
        }

        int m = mat.length;
        int n = mat[0].length;
        int[][] dirs = {{-1, 1}, {1, -1}};

        int row = 0;
        int col = 0;
        int di = 0;
        int[] res = new int[m * n];

        for (int i = 0; i < m * n; i++) {
            res[i] = mat[row][col];

            row = row + dirs[di][0];
            col = col + dirs[di][1];

            if (col >= n) {
                col = n - 1;
                row += 2;
                di = 1 - di;
            }
            if (row >= m) {
                row = m - 1;
                col += 2;
                di = 1 - di;
            }
            if (col < 0) {
                col = 0;
                di = 1 - di;
            }
            if (row < 0) {
                row = 0;
                di = 1 - di;
            }
        }

        return res;
    }
}
```
