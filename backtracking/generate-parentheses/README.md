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
        if (n <= 0) {
            return new ArrayList<>();
        }

        int leftCount = 0;
        int rightCount = 0;
        StringBuilder sb = new StringBuilder();
        List<String> res = new ArrayList<>();

        generateParenthesisUtil(n, leftCount, rightCount, sb, res);

        return res;
    }

    private void generateParenthesisUtil(int n, int leftCount, int rightCount, StringBuilder sb, List<String> res) {
        if (rightCount > leftCount) {
            return;
        }

        if (leftCount == n && rightCount == n) {
            res.add(sb.toString());
            return;
        }

        if (leftCount < n) {
            sb.append("(");
            generateParenthesisUtil(n, leftCount + 1, rightCount, sb, res);
            sb.deleteCharAt(sb.length() - 1);
        }

        if (rightCount < n) {
            sb.append(")");
            generateParenthesisUtil(n, leftCount, rightCount + 1, sb, res);
            sb.deleteCharAt(sb.length() - 1);
        }
    }
}
```

## Solution 2

```java
/**
 * Question   : 22. Generate Parentheses
 * Complexity : Time: O(2^n) ; Space: O(n)
 * Topics     : Backtracking
 */
class Solution {
    public List<String> generateParenthesis(int n) {
        if (n <= 0) {
            return new ArrayList<>();
        }

        int open = 0;
        int close = 0;
        StringBuilder sb = new StringBuilder();
        List<String> res = new ArrayList<>();

        generateParenthesisUtil(n, open, close, sb, res);

        return res;
    }

    private void generateParenthesisUtil(int n, int open, int close, StringBuilder sb, List<String> res) {
        if (open > n || close > open) {
            return;
        }
        if (open == n && close == n) {
            res.add(sb.toString());
            return;
        }

        sb.append("(");
        generateParenthesisUtil(n, open + 1, close, sb, res);
        sb.deleteCharAt(sb.length() - 1);

        sb.append(")");
        generateParenthesisUtil(n, open, close + 1, sb, res);
        sb.deleteCharAt(sb.length() - 1);
    }
}
```
