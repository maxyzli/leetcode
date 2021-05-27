# Wildcard Matching

## Solution 1

```java
/**
 * Question   : 44. Wildcard Matching
 * Complexity : Time: O(m*n) ; Space: O(m*n)
 * Topics     : DP
 */
public class Solution {
    public boolean isMatch(String s, String p) {
        boolean[][] dp = new boolean[s.length() + 1][p.length() + 1];

        for (int i = 0; i <= s.length(); i++) {
            for (int j = 0; j <= p.length(); j++) {
                // Initialization: No any characters and patterns.
                if (i == 0 && j == 0) {
                    dp[i][j] = true;
                    continue;
                }

                // Initialization: one of them is empty.
                if (i == 0 || j == 0) {
                    if (i == 0) { // No any characters.
                        if (p.charAt(j - 1) == '*') {
                            dp[i][j] = dp[i][j - 1]; // * matches 0 character.
                        } else {
                            dp[i][j] = false;
                        }
                    } else if (j == 0) { // No any patterns.
                        dp[i][j] = false;
                    }
                    continue;
                }

                if (p.charAt(j - 1) == '*') {
                    // dp[i][j - 1]: '*' matches no character.
                    // dp[i - 1][j]: '*' matches the character at i and `reuse again` to match s character at i - 1.
                    dp[i][j] = dp[i][j - 1] || dp[i - 1][j];
                } else if (p.charAt(j - 1) == '?') { // '?' always matches with s.charAt(i).
                    dp[i][j] = dp[i - 1][j -  1];
                } else { // Match character with character.
                    if (s.charAt(i - 1) == p.charAt(j - 1)) {
                        dp[i][j] = dp[i - 1][j -  1];
                    } else {
                        dp[i][j] = false;
                    }
                }
            }
        }

        //     0 1 2 3 4
        //     " * a * b
        // 0 " T T F F F
        // 1 a F T T T F
        // 2 d F
        // 3 c F
        // 4 e F
        // 5 b F

        return dp[s.length()][p.length()];
    }
}
```
