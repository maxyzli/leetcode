# Palindromic Substrings

## Solution 1

Brute Force

```java
/**
 * Question   : 647. Palindromic Substrings
 * Complexity : Time: O(n^3) ; Space: O(1)
 * Topics     : DP
 */
public class Solution {
    public int countSubstrings(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }

        int n = s.length();

        int count = 0;

        for (int i = 0; i < n; i++) {
           for (int j = i; j < n; j++) {
               if (isPalindrom(s, i, j)) {
                   count++;
               }
           }
        }

        return count;
    }

    private boolean isPalindrom(String s, int i, int j) {
        while (i < j) {
            if (s.charAt(i) != s.charAt(j)) {
                return false;
            }
            i++;
            j--;
        }
        return true;
    }
}
```

## Solution 2

DP

```java
/**
 * Question   : 647. Palindromic Substrings
 * Complexity : Time: O(n^2) ; Space: O(n^2)
 * Topics     : DP
 */
public class Solution {
    public int countSubstrings(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }

        int n = s.length();

        boolean[][] memo = new boolean[n][n];
        int count = 0;

        for (int len = 1; len <= n; len++) {
            for (int i = 0; i < n - len + 1; i++) {
                int j = i + len - 1;

                if (len == 1) {
                    memo[i][j] = true;
                    count++;
                } else if (len == 2) {
                    if (s.charAt(i) == s.charAt(j)) {
                        memo[i][j] = true;
                        count++;
                    }
                } else { // len >= 3
                    if (s.charAt(i) == s.charAt(j) && memo[i + 1][j - 1]) {
                        memo[i][j] = true;
                        count++;
                    }
                }
            }
        }

        return count;
    }
}
```
