# Coin Change 2

## Solution 1

Two dimensional array

```java
/**
 * Question   : Coin Change 2
 * Complexity : Time: O(m*n) ; Space: O(m*n)
 * Topics     : DP
 * Date       : 2021/01/21
 */
class Solution {
    public int change(int n, int[] coins) {
        int[][] dp = new int[coins.length + 1][n + 1];

        for (int i = 0; i <= coins.length; i++) {
            dp[i][0] = 1;
        }

        for (int i = 1; i <= coins.length; i++) {
            for (int amount = 1; amount <= n; amount++) {
                if (amount >= coins[i - 1]) {
                    dp[i][amount] = dp[i - 1][amount] + dp[i][amount - coins[i - 1]];
                } else {
                    dp[i][amount] = dp[i - 1][amount];
                }
            }
        }

        return dp[coins.length][n];
    }
}
```

## Solution 2

One dimensional array (State Compression)

```java
/**
 * Question   : 518. Coin Change 2
 * Topics     : DP
 * Complexity : Time: O(n*amount) ; Space: O(amount)
 */
class Solution {
    public int change(int amount, int[] coins) {
        if (coins == null || amount < 0) {
            return 0;
        }

        int[] memo = new int[amount + 1];
        memo[0] = 1;

        // For each iteration, use the same coin to make up different amounts.
        for (int i = 0; i < coins.length; i++) {
            for (int currAmount = 1; currAmount <= amount; currAmount++) {
                if (currAmount >= coins[i]) {
                    memo[currAmount] += memo[currAmount - coins[i]];
                }
            }
        }

        return memo[amount];
    }
}
```
