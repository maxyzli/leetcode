# Combination Sum IV

## Solution 1

DFS

```java
/**
 * Question   : 377. Combination Sum IV
 * Complexity : Time: O(n^m) ; Space: O(n)
 * Topics     : DFS, DP
 */
class Solution {
    public int combinationSum4(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        return findCombination(nums, target);
    }

    private int findCombination(int[] nums, int sum) {
        // Base cases
        if (sum == 0) {
            return 1;
        }
        if (sum < 0) {
            return 0;
        }

        int count = 0;
        for (int i = 0; i < nums.length; i++) {
            count += findCombination(nums, sum - nums[i]);
        }

        return count;
    }
}
```

## Solution 2

DP

```java
/**
 * Question   : 377. Combination Sum IV
 * Complexity : Time: O(n*target) ; Space: O(n)
 * Topics     : DFS, DP
 */
class Solution {
    public int combinationSum4(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int n = nums.length;

        // dp[i]: how many combinations for i.
        int[] dp = new int[target + 1];
        dp[0] = 1;

        for (int currTarget = 1; currTarget <= target; currTarget++) {
            for (int i = 0; i < n; i++) {
                if (currTarget >= nums[i]) {
                    dp[currTarget] += dp[currTarget - nums[i]];
                }
            }
        }
        
        return dp[target];
    }
}
```
