# Edit Distance

## Solution 1

```java
/**
 * Question   : 72. Edit Distance
 * Complexity : Time: O(m*n) ; Space: O(m*n)
 * Topics     : DP
 */
public class Solution {
    public int minDistance(String word1, String word2) {
        int[][] dp = new int[word1.length() + 1][word2.length() + 1];

        // Note: We try to transform word1 to word2.

        for (int i = 0; i <= word1.length(); i++) {
            for (int j = 0; j <= word2.length(); j++) {
                // Initialization: No any character.
                if (i == 0 && j == 0) {
                    continue;
                }

                // Initialization: One of the word is empty.
                if (i == 0 || j == 0) {
                    if (i == 0) {
                        dp[i][j] = 1 + dp[i][j - 1]; // all insert.
                    }
                    if (j == 0) {
                        dp[i][j] = 1 + dp[i - 1][j]; // all delete.
                    }
                    continue;
                }

                if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    int insertChar = 1 + dp[i - 1][j];
                    int deleteChar = 1 + dp[i][j - 1];
                    int replaceChar = 1 + dp[i - 1][j - 1];
                    dp[i][j] = Math.min(Math.min(insertChar, deleteChar), replaceChar);
                }
            }
        }

        return dp[word1.length()][word2.length()];
    }

    // right: insert
    // down: delete
    // up-left: replace

    //     0 1 2 3
    //     " r o s
    // 0 " 0 1 2 3
    // 1 h 1 1
    // 2 o 2
    // 3 r 3
    // 4 s 4
    // 5 e 5
}
```
