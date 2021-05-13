# Integer Break

## Solution 1

```java
/**
 * Question   : 343. Integer Break
 * Complexity : Time: O(m*n) ; Space: O(n)
 * Topics     : DP
 */
class Solution {
    public int integerBreak(int n) {
        int[] dp = new int[n + 1];
        dp[1] = 1;

        for (int i = 2; i <= n; i++) {
            for (int j = 1; j < i; j++) {
                dp[i] = Math.max(dp[i], Math.max((i - j) * j, dp[i - j] * j));
            }
        }

        return dp[n];
    }
}
```
