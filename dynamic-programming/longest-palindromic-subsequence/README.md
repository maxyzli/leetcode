# Longest Palindromic Subsequence

## Solution 1

DP use length forward.

```jsx
/**
 * Question   : 516. Longest Palindromic Subsequence
 * Topics     : DP
 * Complexity : Time: O(n^2) ; Space: O(n^2)
 */
public class Solution {
    public int longestPalindromeSubseq(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }

        int n = s.length();

        int[][] memo = new int[n][n];

        // Initialization.
        for (int i = 0; i < n; i++) {
            memo[i][i] = 1;
        }
        // Check length >= 2.
        for (int i = 0; i < n - 1; i++) {
            if (s.charAt(i) == s.charAt(i + 1)) {
                memo[i][i + 1] = 2;
            } else {
                memo[i][i + 1] = 1;
            }
        }

        // Check length >= 3.
        for (int len = 2; len <= n; len++) {
            for (int i = 0; i < n - len + 1; i++) {
                // since i < n - len + 1;
                // j = i + len - 1 => j < (n - len + 1) + len - 1 => j < n;
                int j = i + len - 1;
                if (s.charAt(i) == s.charAt(j)) {
                    memo[i][j] = 2 + memo[i + 1][j - 1];
                } else {
                    memo[i][j] = Math.max(memo[i + 1][j], memo[i][j - 1]);
                }
            }
        }

        return memo[0][n - 1];
    }
}
```

## Solution 2

DP From backward.

```java
/**
 * Question   : 516. Longest Palindromic Subsequence
 * Topics     : DP
 * Complexity : Time: O(n^2) ; Space: O(n^2)
 */
public class Solution {
    public int longestPalindromeSubseq(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }

        int n = s.length();

        int[][] memo = new int[n][n];

        // Initialization.
        for (int i = 0; i < n; i++) {
            memo[i][i] = 1;
        }

        // Check length >= 2.
        // From backward.
        for (int i = s.length() - 1; i >= 0; i--) {
            for (int j = i + 1; j < s.length(); j++) {
                if (s.charAt(i) == s.charAt(j)) {
                    memo[i][j] = 2 + memo[i + 1][j - 1];
                } else {
                    memo[i][j] = Math.max(memo[i + 1][j], memo[i][j - 1]);
                }
            }
        }

        return memo[0][n - 1];
    }
}
```
