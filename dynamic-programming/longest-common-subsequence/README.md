# Longest Common Subsequence

## Solution 1

DFS

```java
/**
 * Question   : 1143. Longest Common Subsequence
 * Complexity : Time: O(2^n) ; Space: O(n)
 * Topics     : DP
 */
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        int n1 = text1.length();
        int n2 = text2.length();
        return longestCommonSubsequenceUtil(text1, n1, text2, n2);
    }

    private int longestCommonSubsequenceUtil(String text1, int n1, String text2, int n2) {
        if (n1 == 0 || n2 == 0) {
            return 0;
        }

        if (text1.charAt(n1 - 1) == text2.charAt(n2 - 1)) {
            return 1 + longestCommonSubsequenceUtil(text1, n1 - 1, text2, n2 - 1);
        } else {
            return Math.max(
                    longestCommonSubsequenceUtil(text1, n1 - 1, text2, n2),
                    longestCommonSubsequenceUtil(text1, n1, text2, n2 - 1)
            );
        }
    }
}
```

## Solution 2

DP

```java
/**
 * Question   : 1143. Longest Common Subsequence
 * Complexity : Time: O(n^2) ; Space: O(n^2)
 * Topics     : DP
 */
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        int n1 = text1.length();
        int n2 = text2.length();

        // dp[i][j]: Longest common subsequence given i and j indexes.
        int[][] dp = new int[n1 + 1][n2 + 1];

        for (int i = 1; i <= n1; i++) {
            for (int j = 1; j <= n2; j++) {
                if (text1.charAt(i - 1) == text2.charAt(j - 1)) {
                    dp[i][j] = 1 + dp[i - 1][j - 1];
                } else {
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }

        return dp[n1][n2];
    }
}
```
