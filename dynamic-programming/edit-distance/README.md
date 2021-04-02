# Edit Distance

## Solution 1

```java
/**
 * Question   : Edit Distance
 * Complexity : Time: O(m*n) ; Space: O(m*n)
 * Topics     : DP
 * Date       : 2021/01/04
 */
class Solution {
    public int minDistance(String word1, String word2) {
        int l1 = word1.length();
        int l2 = word2.length();

        int[][] dp = new int[l1 + 1][l2 + 1];

        for (int i = 0; i <= l1; i++) {
            dp[i][0] = i;
        }
        for (int j = 0; j <= l2; j++) {
            dp[0][j] = j;
        }

        for (int i = 1; i <= l1; i++) {
            for (int j = 1; j <= l2; j++) {
                // If the latest character is the same, the edit distance is the same as previous one.
                if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                    continue;
                }

                int insert = dp[i][j - 1];       // (Make str1 the same as str2 - 1), so we need to insert the new character.
                int delete = dp[i - 1][j];       // (Make str1 - 1 the same as str2), so we need to delete the new character.
                int replace = dp[i - 1][j - 1];  // (Make str1 - 1 the same as str2 - 1), so we need to check if we need to replace the latest character.

                dp[i][j] = 1 + Math.min(insert, Math.min(delete, replace));
            }
        }

        return dp[l1][l2];
    }
}
```
