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
        boolean[][] memo = new boolean[s.length() + 1][p.length() + 1];

        for (int i = 0; i <= s.length(); i++) {
            for (int j = 0; j <= p.length(); j++) {
                // Initialization: No any characters and patterns.
                if (i == 0 && j == 0) {
                    memo[i][j] = true;
                    continue;
                }

                // Initialization: one of them is empty.
                if (i == 0 || j == 0) {
                    if (i == 0) { // No any characters.
                        if (p.charAt(j - 1) == '*') {
                            memo[i][j] = memo[i][j - 1]; // * matches 0 character.
                        } else {
                            memo[i][j] = false;
                        }
                    } else if (j == 0) { // No any patterns.
                        memo[i][j] = false;
                    }
                    continue;
                }

                if (p.charAt(j - 1) == '*') {
                    // memo[i][j - 1]: '*' matches no character.
                    // memo[i - 1][j]: '*' matches the character at i and `reuse again` to match s character at i - 1.
                    memo[i][j] = memo[i][j - 1] || memo[i - 1][j];
                } else if (p.charAt(j - 1) == '?') { // '?' always matches with s.charAt(i).
                    memo[i][j] = memo[i - 1][j -  1];
                } else { // Match character with character.
                    if (s.charAt(i - 1) == p.charAt(j - 1)) {
                        memo[i][j] = memo[i - 1][j -  1];
                    } else {
                        memo[i][j] = false;
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

        return memo[s.length()][p.length()];
    }
}
```
