# Longest Palindromic Subsequence

## Solution 1

DFS

```java
/**
 * Question   : 516. Longest Palindromic Subsequence
 * Complexity : Time: O(2^n) ; Space: O(n)
 * Topics     : DP
 */
class Solution {
    int longest;

    public int longestPalindromeSubseq(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }

        longest = 0;

        StringBuilder sb = new StringBuilder();
        int beginIndex = 0;
        longestPalindromeSubseq(s, beginIndex, sb);

        return longest;
    }

    private void longestPalindromeSubseq(String s, int beginIndex, StringBuilder sb) {
        if (isPalindrome(sb.toString())) {
            longest = Math.max(longest, sb.toString().length());
        }

        for (int i = beginIndex; i < s.length(); i++) {
            sb.append(s.charAt(i));
            longestPalindromeSubseq(s, i + 1, sb);
            sb.deleteCharAt(sb.length() - 1);
        }
    }

    private boolean isPalindrome(String s) {
        if (s == "") {
            return true;
        }

        int left = 0;
        int right = s.length() - 1;

        while (left < right) {
            if (s.charAt(left) != s.charAt(right)) {
                return false;
            }
            left++;
            right--;
        }

        return true;
    }
}
```

## Solution 2

DP use length forward.

```java
/**
 * Question   : 516. Longest Palindromic Subsequence
 * Complexity : Time: O(n^2) ; Space: O(n^2)
 * Topics     : DP
 */
class Solution {
    public int longestPalindromeSubseq(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }

        int n = s.length();

        int[][] dp = new int[n][n];

        for (int len = 1; len <= n; len++) {
            for (int i = 0; i < n - len + 1; i++) {
                int j = i + len - 1;

                if (len == 1) {
                    dp[i][j] = 1;
                } else if (len == 2) {
                    if (s.charAt(i) == s.charAt(j)) {
                        dp[i][j] = 2;
                    } else {
                        dp[i][j] = 1;
                    }
                } else {
                    if (s.charAt(i) == s.charAt(j)) {
                       dp[i][j] = 2 + dp[i + 1][j - 1];
                    } else {
                        dp[i][j] = Math.max(dp[i + 1][j], dp[i][j - 1]);
                    }
                }
            }
        }

        return dp[0][n - 1];
    }
}
```

## Solution 3

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

        int[][] dp = new int[n][n];

        // Initialization.
        for (int i = 0; i < n; i++) {
            dp[i][i] = 1;
        }

        // Check length >= 2.
        // From backward.
        for (int i = s.length() - 1; i >= 0; i--) {
            for (int j = i + 1; j < s.length(); j++) {
                if (s.charAt(i) == s.charAt(j)) {
                    dp[i][j] = 2 + dp[i + 1][j - 1];
                } else {
                    dp[i][j] = Math.max(dp[i + 1][j], dp[i][j - 1]);
                }
            }
        }

        return dp[0][n - 1];
    }
}
```
