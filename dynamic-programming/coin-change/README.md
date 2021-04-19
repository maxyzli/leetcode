# Coin Change

## Solution 1

DFS (Time Limit Exceeded)

```java
/**
 * Question   : 322. Coin Change
 * Topics     : DP
 * Complexity : Time: O(n^amount) ; Space: O(amount)
 */
public class Solution {
    int minCount;

    public int coinChange(int[] coins, int amount) {
        if (coins == null || amount == 0) {
            return 0;
        }

        minCount = Integer.MAX_VALUE;

        coinChange(coins, amount, 0);

        return minCount == Integer.MAX_VALUE ? -1 : minCount;
    }

    private void coinChange(int[] coins, int amount, int count) {
        if (amount == 0) {
            minCount = Math.min(minCount, count);
            return;
        }
        for (int i = 0; i < coins.length; i++) {
            if (coins[i] <= amount) {
                coinChange(coins, amount - coins[i], count + 1);
            }
        }
    }
}
```

## Solution 2

DFS function return minimum count (Time Limit Exceeded)

```java
/**
 * Question   : 322. Coin Change
 * Topics     : DP
 * Complexity : Time: O(n^amount) ; Space: O(amount)
 */
class Solution {
    public int coinChange(int[] coins, int amount) {
        if (coins == null || coins.length == 0 || amount == 0) {
            return 0;
        }

        int min = Integer.MAX_VALUE;
        for (int i = 0; i < coins.length; i++) {
            if (amount >= coins[i]) {
                int subMinCount = coinChange(coins, amount - coins[i]);
                if (subMinCount == -1) {
                    continue;
                }
                min = Math.min(min, subMinCount + 1);
            }
        }

        return min == Integer.MAX_VALUE ? -1 : min;
    }
}
```

## Solution 3

Top-Down DP

```java
/**
 * Question   : 322. Coin Change
 * Topics     : DP
 * Complexity : Time: O(n*amount) ; Space: O(amount)
 */
class Solution {
    int[] memo;

    public int coinChange(int[] coins, int amount) {
        if (coins == null || coins.length == 0 || amount == 0) {
            return 0;
        }
        memo = new int[amount + 1];
        Arrays.fill(memo, Integer.MAX_VALUE);
        coinChangeUtil(coins, amount);
        return memo[amount];
    }

    public int coinChangeUtil(int[] coins, int amount) {
        if (coins == null || coins.length == 0 || amount == 0) {
            return 0;
        }

        if (memo[amount] != Integer.MAX_VALUE) {
            return memo[amount];
        }

        int min = Integer.MAX_VALUE;
        for (int i = 0; i < coins.length; i++) {
            if (amount >= coins[i]) {
                int subMinCount = coinChangeUtil(coins, amount - coins[i]);
                if (subMinCount == -1) {
                    continue;
                }
                min = Math.min(min, subMinCount + 1);
            }
        }

        memo[amount] = (min == Integer.MAX_VALUE ? -1 : min);

        return memo[amount];
    }
}
```

## Solution 4

Bottom-Up DP

```java
import java.util.*;

/**
 * Question   : 322. Coin Change
 * Topics     : DP
 * Complexity : Time: O(n*amount) ; Space: O(amount)
 */
class Solution {
    public int coinChange(int[] coins, int amount) {
        if (coins == null || coins.length == 0 || amount <= 0) {
            return 0;
        }

        int[] memo = new int[amount + 1];
        Arrays.fill(memo, Integer.MAX_VALUE);

        memo[0] = 0;

        // For each iteration, use the same coin to make up different amounts.
        for (int i = 0; i < coins.length; i++) {
            for (int currAmount = 1; currAmount <= amount; currAmount++) {
                if (currAmount >= coins[i]) {
                    if (memo[currAmount - coins[i]] == Integer.MAX_VALUE) {
                        continue;
                    }
                    memo[currAmount] = Math.min(memo[currAmount], memo[currAmount - coins[i]] + 1);
                }
            }
        }

        return memo[amount] == Integer.MAX_VALUE ? -1 : memo[amount];
    }
}
```

## Solution 5

Bottom-Up DP 2

```java
/**
 * Question   : 322. Coin Change
 * Topics     : DP
 * Complexity : Time: O(n*amount) ; Space: O(amount)
 */
class Solution {
    public int coinChange(int[] coins, int amount) {
        if (coins == null || coins.length == 0 || amount <= 0) {
            return 0;
        }

        int[] memo = new int[amount + 1];
        Arrays.fill(memo, Integer.MAX_VALUE);

        memo[0] = 0;

        // For each iteration, we use the same amount and try to make up by different coins.
        for (int currAmount = 1; currAmount <= amount; currAmount++) {
            for (int i = 0; i < coins.length; i++) {
                if (currAmount >= coins[i]) {
                    if (memo[currAmount - coins[i]] == Integer.MAX_VALUE) {
                        continue;
                    }
                    memo[currAmount] = Math.min(memo[currAmount], memo[currAmount - coins[i]] + 1);
                }
            }
        }

        // This solution will generate duplicate combination. (Won't able to solve Coin Change 2)
        // example: coins [1,2], amount 3
        // will generate: [1,2], [2,1] which are duplicates.

        return memo[amount] == Integer.MAX_VALUE ? -1 : memo[amount];
    }
}
```
