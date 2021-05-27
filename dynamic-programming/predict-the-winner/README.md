# Predict the Winner

## Solution 1

DFS (Calculate at Returning Phase)

```java
/**
 * Question   : 486. Predict the Winner
 * Complexity : Time: O(2^n) ; Space: O(n)
 * Topics     : DP
 */
public class Solution {
    public boolean PredictTheWinner(int[] nums) {
        if (nums == null || nums.length == 0) {
            return false;
        }

        int beginIndex = 0;
        int endIndex = nums.length - 1;

        return predictTheWinner(nums, beginIndex, endIndex) >= 0;
    }

    private int predictTheWinner(int[] nums, int beginIndex, int endIndex) {
        if (beginIndex == endIndex) {
            return nums[beginIndex];
        }
        int leftOpponentsScore = predictTheWinner(nums, beginIndex + 1, endIndex);
        int rightOpponentsScore = predictTheWinner(nums, beginIndex, endIndex - 1);
        return Math.max(nums[beginIndex] - leftOpponentsScore, nums[endIndex] - rightOpponentsScore);
    }
}
```

## Solution 2

Top-Down DP

```java
/**
 * Question   : 486. Predict the Winner
 * Complexity : Time: O(n^2) ; Space: O(n^2)
 * Topics     : DP
 */
public class Solution {
    public boolean PredictTheWinner(int[] nums) {
        if (nums == null || nums.length == 0) {
            return false;
        }

        int[][] dp = new int[nums.length][nums.length];
        for (int i = 0; i < nums.length; i++) {
            Arrays.fill(dp[i], Integer.MIN_VALUE);
        }

        int beginIndex = 0;
        int endIndex = nums.length - 1;

        return predictTheWinner(nums, beginIndex, endIndex, dp) >= 0;
    }

    private int predictTheWinner(int[] nums, int beginIndex, int endIndex, int[][] dp) {
        if (beginIndex == endIndex) {
            return nums[beginIndex];
        }

        if (dp[beginIndex][endIndex] != Integer.MIN_VALUE) {
            return dp[beginIndex][endIndex];
        }

        int leftOpponentsScore = predictTheWinner(nums, beginIndex + 1, endIndex, dp);
        int rightOpponentsScore = predictTheWinner(nums, beginIndex, endIndex - 1, dp);

        int myScore = Math.max(nums[beginIndex] - leftOpponentsScore, nums[endIndex] - rightOpponentsScore);
        dp[beginIndex][endIndex] = myScore;

        return dp[beginIndex][endIndex];
    }
}
```

## Solution 3

Bottom-Up DP

```java
/**
 * Question   : 486. Predict the Winner
 * Complexity : Time: O(n^2) ; Space: O(n^2)
 * Topics     : DP
 */
class Solution {
    public boolean PredictTheWinner(int[] nums) {
        int n = nums.length;

        // dp[i][j] means the maximum value the player can win at i, j interval.
        int[][] dp = new int[n][n];

        // Initialization: Only one value can choose from.
        for (int i = 0; i < n; i++) {
            dp[i][i] = nums[i];
        }

        for (int interval = 2; interval <= n; interval++) {
            for (int i = 0; i < n - interval + 1; i++) {
                int j = i + interval - 1;
                // Player can choose either index i or index j.
                dp[i][j] = Math.max(nums[i] - dp[i + 1][j], nums[j] - dp[i][j - 1]);
            }
        }

        return dp[0][n - 1] >= 0;
    }
}
```
