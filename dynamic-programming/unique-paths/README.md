# Unique Paths

## Solution 1

Two Dimensional Array

```java
/**
 * Question   : 62. Unique Paths
 * Complexity : Time: O(m*n) ; Space: O(m*n)
 * Topics     : DP
 */
class Solution {
    public int uniquePaths(int m, int n) {
        int[][] dp = new int[m][n];
        dp[0][0] = 1;

        for (int i = 1; i < m; i++) {
            dp[i][0] = dp[i - 1][0];
        }
        for (int j = 1; j < n; j++) {
            dp[0][j] = dp[0][j - 1];
        }

        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
            }
        }

        return dp[m - 1][n - 1];
    }
}
```

## Solution 2

One Dimensional Array

```java
/**
 * Question   : 62. Unique Paths
 * Complexity : Time: O(m*n) ; Space: O(n)
 * Topics     : DP
 */
class Solution {
    public int uniquePaths(int m, int n) {
        int[] dp = new int[n];
        dp[0] = 1;

        for (int j = 1; j < n; j++) {
            dp[j] = dp[j - 1];
        }

        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[j] += dp[j - 1];
            }
        }

        return dp[n - 1];
    }
}
```

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8dad7d7e-321c-4868-b229-98d7aa713e0a/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8dad7d7e-321c-4868-b229-98d7aa713e0a/Untitled.png)
