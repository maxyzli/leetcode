# Generate Parentheses

## Solution 1

```java
/**
 * Question   : 22. Generate Parentheses
 * Complexity : Time: O(2^n) ; Space: O(n)
 * Topics     : Backtracking
 */
class Solution {
    public List<String> generateParenthesis(int n) {
        if (n == 0) {
            return new LinkedList<>();
        }

        List<String> res = new LinkedList<>();
        StringBuilder sb = new StringBuilder();
        int left = 0;
        int right = 0;

        dfs(sb, left, right, n, res);

        return res;
    }


    private void dfs(StringBuilder sb, int left, int right, int n, List<String> res) {
        if (left + right == n * 2) {
            res.add(sb.toString());
            return;
        }

        if (left < n) {
            sb.append('(');
            dfs(sb, left + 1, right, n, res);
            sb.deleteCharAt(sb.length() - 1);
        }

        if (left > right) {
            sb.append(')');
            dfs(sb, left, right + 1, n, res);
            sb.deleteCharAt(sb.length() - 1);
        }
    }
}
```
