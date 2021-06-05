# Coin Change

## Solution 1

DFS (Time Limit Exceeded)

```java
/**
 * Question   : 322. Coin Change
 * Complexity : Time: O(2^n) ; Space: O(n)
 * Topics     : DP
 */
class Solution {
    public int coinChange(int[] coins, int amount) {
        if (coins == null || coins.length == 0) {
            return -1;
        }
        return coinChangeUtil(coins, amount, coins.length);
    }

    private int coinChangeUtil(int[] coins, int amount, int n) {
        // Base cases
        if (amount == 0) {
            return 0;
        }
        if (amount < 0 || n == 0) {
            return Integer.MAX_VALUE;
        }

        if (coins[n - 1] > amount) {
            return coinChangeUtil(coins, amount, n - 1);
        }

        int option1 = coinChangeUtil(coins, amount - coins[n - 1], n);
        int option2 = coinChangeUtil(coins, amount, n - 1);

        if (option1 != Integer.MAX_VALUE && option2 != Integer.MAX_VALUE) {
            return Math.min(1 + option1, option2);
        } else if (option1 == Integer.MAX_VALUE) {
            return option2;
        } else {
            return 1 + option1;
        }
    }
}
```

## Solution 2

Bottom-Up DP

```java
/**
 * Question   : 322. Coin Change
 * Complexity : Time: O(n*amount) ; Space: O(n)
 * Topics     : DP
 */
public class Solution {
    public int coinChange(int[] coins, int amount) {
        if (coins == null || coins.length == 0) {
            return -1;
        }

        int n = coins.length;

        // dp[j]: minimum coins to make up j.
        int[] dp = new int[amount + 1];

        // Initialization.
        Arrays.fill(dp, Integer.MAX_VALUE);
        dp[0] = 0;

        for (int i = 1; i <= n; i++) {
            for (int currAmount = 1; currAmount <= amount; currAmount++) {
                if (currAmount >= coins[i - 1]) {
                    int subMinCoins = dp[currAmount - coins[i - 1]];
                    if (subMinCoins != Integer.MAX_VALUE) {
                        dp[currAmount] = Math.min(dp[currAmount], 1 + subMinCoins);
                    }
                }
            }
        }

        return dp[amount] == Integer.MAX_VALUE ? -1 : dp[amount];
    }
}
```
