# ZigZag Conversion

## Solution 1

Matrix

```java
/**
 * Question   : 6. ZigZag Conversion
 * Complexity : Time: O(n) ; Space: O(n^2)
 * Topics     : Array
 */
public class Solution {
    public String convert(String s, int numRows) {
        int[][] matrix = new int[numRows][s.length()];

        if (numRows == 1) {
            return s;
        }

        int row = 0;
        int col = 0;

        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            matrix[row][col] = c;
            if ((col % (numRows - 1)) == 0) {
                if (row == numRows - 1) {
										// If we are at the last row, go to next column.
                    row--;
                    col++;
                } else {
                    row++;
                }
            } else {
                row--;
                col++;
            }
        }

        StringBuilder sb = new StringBuilder();
        for (int r = 0; r < numRows; r++) {
            for (int c = 0; c < s.length(); c++) {
                if (matrix[r][c] != 0) {
                    sb.append((char)matrix[r][c]);
                }
            }
        }

        return sb.toString();
    }
}
```

## Solution 2

StringBuilder

```java
/**
 * Question   : 6. ZigZag Conversion
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Array
 */
public class Solution {
    public String convert(String s, int numRows) {
        StringBuilder[] sbs = new StringBuilder[numRows];
        for (int i = 0; i < sbs.length; i++) {
            sbs[i] = new StringBuilder();
        }

        int n = s.length();
        int i = 0;

        while (i < n) {
            // Vertical
            for (int idx = 0; idx < numRows && i < n; idx++) {
                sbs[idx].append(s.charAt(i++));
            }

            for (int idx = numRows - 2; idx >= 1 && i < n; idx--) {
                sbs[idx].append(s.charAt(i++));
            }
        }

        StringBuilder res = new StringBuilder();
        for (int j = 0; j < sbs.length; j++) {
            res.append(sbs[j]);
        }

        return res.toString();
    }
}
```
