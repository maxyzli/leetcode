# Distinct Subsequences

## Solution 1

Brute Force

```java
/**
 * Question   : 115. Distinct Subsequences
 * Complexity : Time: O(exp) ; Space: O(m+n)
 * Topics     : DP
 */
class Solution {
    public int numDistinct(String S, String T) {
        return find(S, 0, T, 0, 0);
    }

    private int find(String S, int i, String T, int j, int currMatchCount) {
        if (currMatchCount == T.length()) {
            return 1;
        }

        if (i >= S.length() || j >= T.length()) {
            return 0;
        }

        if (S.charAt(i) == T.charAt(j)) {
            return find(S, i + 1, T, j + 1, currMatchCount + 1) + find(S, i + 1, T, j, currMatchCount);
        }

        return find(S, i + 1, T, j, currMatchCount);
    }
}
```

## Solution 2

DP

```java
/**
 * Question   : 115. Distinct Subsequences
 * Complexity : Time: O(m*n) ; Space: O(m*n)
 * Topics     : DP
 */
class Solution {
    public int numDistinct(String s, String t) {
        int[][] memo = new int[t.length()][s.length()];

        // Try to generate t from s.

        //     (s) b a b g b a g
        // (t)
        //  b      1 1 2 2 3 3 3
        //  a      0
        //  g      0

        if (s.charAt(0) == t.charAt(0)) {
            memo[0][0] = 1;
        }

        for (int j = 1; j < s.length(); j++) {
            if (s.charAt(j) == t.charAt(0)) {
                memo[0][j] = memo[0][j - 1] + 1;
            } else {
                memo[0][j] = memo[0][j - 1];
            }
        }

        for (int i = 1; i < t.length(); i++) {
            for (int j = 1; j < s.length(); j++) {
                if (s.charAt(j) == t.charAt(i)) {
                    memo[i][j] = memo[i - 1][j - 1] + memo[i][j - 1];
                } else {
                    memo[i][j] = memo[i][j - 1];
                }
            }
        }

        return memo[t.length() - 1][s.length() - 1];
    }
}
```
