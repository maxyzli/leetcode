# Partition Equal Subset Sum

## Solution 1

DFS

```java
/**
 * Question   : 416. Partition Equal Subset Sum
 * Complexity : Time: O(2^n) ; Space: O(n)
 * Topics     : DP
 */
class Solution {
    public boolean canPartition(int[] nums) {
        int totalSum = 0;
        for (int num : nums) {
            totalSum += num;
        }

        if (totalSum % 2 != 0) {
            return false;
        }

        return canPartitionUtil(nums, totalSum / 2, nums.length);
    }

    private boolean canPartitionUtil(int[] nums, int sum, int n) {
        if (sum == 0) {
            return true;
        }
        if (sum < 0 || n == 0) {
            return false;
        }

        if (nums[n - 1] > sum) {
            return canPartitionUtil(nums, sum, n - 1);
        }
        return canPartitionUtil(nums, sum - nums[n - 1], n - 1) || canPartitionUtil(nums, sum, n - 1);
    }
}
```

## Solution 2

DP

```java
/**
 * Question   : 416. Partition Equal Subset Sum
 * Complexity : Time: O(n * amount) ; Space: O(n * amount)
 * Topics     : DP
 */
class Solution {
    public boolean canPartition(int[] nums) {
        int totalSum = 0;
        for (int num : nums) {
            totalSum += num;
        }

        if (totalSum % 2 != 0) {
            return false;
        }

        int sum = totalSum / 2;
        int n = nums.length;

        // dp[i][j]: if we can generate j amount using i numbers.
        boolean[][] dp = new boolean[n + 1][sum + 1];
        for (int i = 0; i <= n; i++) {
            dp[i][0] = true;
        }

        for (int i = 1; i <= n; i++) {
            for (int currSum = 1; currSum <= sum; currSum++) {
                if (currSum >= nums[i - 1]) {
                    dp[i][currSum] = dp[i - 1][currSum] || dp[i - 1][currSum - nums[i - 1]];
                } else {
                    dp[i][currSum] = dp[i - 1][currSum];
                }
            }
        }

        return dp[n][sum];
    }
}
```
