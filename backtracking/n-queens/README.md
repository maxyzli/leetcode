# N-Queens

## Solution 1

```java
/**
 * Question   : 51. N-Queens
 * Complexity : Time: O(n!) ; Space: O(n^2)
 * Topics     : Backtracking
 */
class Solution {
    public List<List<String>> solveNQueens(int n) {
        if (n == 0) {
            return new LinkedList<>();
        }

        List<List<String>> res = new LinkedList<>();
        char[][] table = new char[n][n];
        int col = 0;

        for (int i = 0; i < table.length; i++) {
            Arrays.fill(table[i], '.');
        }

        dfs(table, col, res);

        return res;
    }

    private void dfs(char[][] table, int col, List<List<String>> res) {
        if (col == table.length) {
            res.add(toStringList(table));
            return;
        }

        for (int i = 0; i < table.length; i++) {
            if (isValid(table, i, col)) {
                table[i][col] = 'Q';
                dfs(table, col + 1, res);
                table[i][col] = '.';
            }
        }
    }

    private boolean isValid(char[][] table, int row, int col) {
        // check columns.
        for (int j = 0; j < col; j++) {
            if (table[row][j] == 'Q') {
                return false;
            }
        }

        // Up left
        int i = row - 1;
        int j = col - 1;
        while (i >= 0 && j >= 0) {
            if (table[i][j] == 'Q') {
                return false;
            }
            i--;
            j--;
        }

        // Down left
        i = row + 1;
        j = col - 1;
        while (i < table.length && j >= 0) {
            if (table[i][j] == 'Q') {
                return false;
            }
            i++;
            j--;
        }

        return true;
    }

    private List<String> toStringList(char[][] table) {
        List<String> list = new LinkedList<>();

        for (int i = 0; i < table.length; i++) {
            list.add(String.valueOf(table[i]));
        }

        return list;
    }
}
```
