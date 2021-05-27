# Number of Dice Rolls With Target Sum

# Solution 1

Brute Force

```java
/**
 * Question   : Dice Throw
 * Complexity : Time: O(exponential) ; Space: O(n)
 * Topics     : DP
 */
public class Solution {
    long count = 0;

    public int numRollsToTarget(int d, int f, int target) {
        count = 0;
        numRollsToTargetUtil(d, f, target);
        return (int)(count % (Math.pow(10, 9) + 7));
    }

    private void numRollsToTargetUtil(int d, int f, int target) {
        if (d == 0) {
            if (target == 0) {
                count++;
            }
            return;
        }

        for (int num = 1; num <= f; num++) {
            numRollsToTargetUtil(d - 1, f, target - num);
        }
    }
}
```

# Solution 2

Bottom Up DP

```java
/**
 * Question   : Dice Throw
 * Complexity : Time: O(d*f*target) ; Space: O(d*target)
 * Topics     : DP
 */
class Solution {
    public int numRollsToTarget(int d, int f, int target) {
        int mod = (int)Math.pow(10, 9) + 7;

        int[][] dp = new int[d + 1][target + 1];
        dp[0][0] = 1;

        // i is number of dice
        for (int i = 1; i <= d; i++) {
            // j is the value we want to match
            for (int j = 1; j <= target; j++) {
                // val is the number we throw.
                for (int val = 1; val <= f; val++) {
                    if (j >= val) {
                        dp[i][j] = (dp[i][j] + dp[i - 1][j - val]) % mod;
                    }
                }
            }
        }

        return dp[d][target];
    }
}
```

