# Longest Common Subsequence

## Solution 1

DFS

```java
/**
 * Question   : 1143. Longest Common Subsequence
 * Complexity : Time: O(2^n) ; Space: O(n)
 * Topics     : DP, Backtracking
 */
class Solution {
    int longest = 0;

    public int longestCommonSubsequence(String text1, String text2) {
        longest = 0;
        longestCommonSubsequence(text1, 0, text2, 0, 0);
        return longest;
    }

    private void longestCommonSubsequence(String text1, int p1, String text2, int p2, int count) {
        if (p1 == text1.length() || p2 == text2.length()) {
            return;
        }
        if (text1.charAt(p1) == text2.charAt(p2)) {
            longest = Math.max(longest, count + 1);
            longestCommonSubsequence(text1, p1 + 1, text2, p2 + 1, count + 1);
        } else {
            longestCommonSubsequence(text1, p1 + 1, text2, p2, count);
            longestCommonSubsequence(text1, p1, text2, p2 + 1, count);
        }
    }
}
```

## Solution 2

DFS

```java
/**
 * Question   : 1143. Longest Common Subsequence
 * Complexity : Time: O(2^n) ; Space: O(n)
 * Topics     : DP
 */
public class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        return longestCommonSubsequence(text1, 0, text2, 0);
    }

    private int longestCommonSubsequence(String text1, int i, String text2, int j) {
        if (i >= text1.length() || j >= text2.length()) {
            return 0;
        }

        if (text1.charAt(i) == text2.charAt(j)) {
            return 1 + longestCommonSubsequence(text1, i + 1, text2, j + 1);
        }
        return Math.max(longestCommonSubsequence(text1, i + 1, text2, j), longestCommonSubsequence(text1, i, text2, j + 1));
    }
}
```

## Solution 3

Top-down DP

```java
/**
 * Question   : 1143. Longest Common Subsequence
 * Complexity : Time: O(n^2) ; Space: O(n^2)
 * Topics     : DP
 */
public class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        Integer[][] dprize = new Integer[text1.length() + 1][text2.length() + 1];
        return longestCommonSubsequence(text1, 0, text2, 0, dprize);
    }

    private int longestCommonSubsequence(String text1, int i, String text2, int j, Integer[][] dprize) {
        if (i >= text1.length() || j >= text2.length()) {
            return 0;
        }

        if (dprize[i][j] != null) {
            return dprize[i][j];
        }

        if (text1.charAt(i) == text2.charAt(j)) {
            dprize[i][j] = 1 + longestCommonSubsequence(text1, i + 1, text2, j + 1, dprize);
        } else {
            dprize[i][j] = Math.max(
                    longestCommonSubsequence(text1, i + 1, text2, j, dprize),
                    longestCommonSubsequence(text1, i, text2, j + 1, dprize)
            );
        }

        return dprize[i][j];
    }
}
```

## Solution 4

Bottom-up DP

```java
/**
 * Question   : 1143. Longest Common Subsequence
 * Complexity : Time: O(n^2) ; Space: O(n^2)
 * Topics     : DP
 */
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        if (text1.length() == 0 || text2.length() == 0) {
            return 0;
        }

        int[][] dp = new int[text1.length() + 1][text2.length() + 1];

        for (int i = 1; i <= text1.length(); i++) {
            for (int j = 1; j <= text2.length(); j++) {
                if (text1.charAt(i - 1) == text2.charAt(j - 1)) {
                    dp[i][j] = 1 + dp[i - 1][j - 1];
                } else {
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }

        return dp[text1.length()][text2.length()];
    }
}
```
