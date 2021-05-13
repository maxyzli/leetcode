# Min Cost Climbing Stairs

## Solution 1

```java
/**
 * Question   : 746. Min Cost Climbing Stairs
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : DP
 */
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        if (cost == null || cost.length == 0) {
            return 0;
        }

        int n = cost.length;

        // Minimum cost to reach index i.
        int[] dp = new int[n + 1];
        dp[0] = 0;
        dp[1] = 0;

        for (int i = 2; i <= n; i++) {
            dp[i] = Math.min(dp[i - 2] + cost[i - 2], dp[i - 1] + cost[i - 1]);
        }

        return dp[n];
    }
}
```
