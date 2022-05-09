# House Robber

## Solution 1: DFS

```java
/**
 * Question   : 198. House Robber
 * Complexity : Time: O(2^n) ; Space: O(n)
 * Topics     : DP
 */
class Solution {
    public int rob(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        return robUtil(nums, nums.length);
    }

    private int robUtil(int[] nums, int n) {
        if (n <= 0) {
            return 0;
        }
        return Math.max(nums[n - 1] + robUtil(nums, n - 2), robUtil(nums, n - 1));
    }
}
```

## Solution 2: DP

```java
// TC: O(n)
// SC: O(n)
class Solution {
    public int rob(int[] nums) {
        int n = nums.length;

        int[] dp = new int[n + 1];
        dp[0] = 0;
        dp[1] = nums[0];

        for (int i = 2; i <= n; i++) {
            dp[i] = Math.max(dp[i - 2] + nums[i - 1], dp[i - 1]);
        }

        return dp[n];
    }
}
```

## Solution 3: DP with space compression

```java
// TC: O(n)
// SC: O(1)
class Solution {
    public int rob(int[] nums) {
        int n = nums.length;

        int pre2Day = 0;
        int pre1Day = nums[0];
        int curr = Math.max(pre2Day, pre1Day);

        for (int i = 2; i <= n; i++) {
            curr = Math.max(pre2Day + nums[i - 1], pre1Day);
            pre2Day = pre1Day;
            pre1Day = curr;
        }

        return curr;
    }
}
```
