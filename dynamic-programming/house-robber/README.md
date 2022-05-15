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
        if (nums.length == 1) {
            return nums[0];
        }

        int n = nums.length;

        int[] dp = new int[n];
        dp[0] = nums[0];
        dp[1] = Math.max(nums[0], nums[1]);

        for (int i = 2; i < n; i++) {
            dp[i] = Math.max(dp[i - 2] + nums[i], dp[i - 1]);
        }

        return dp[n - 1];
    }
}
```

## Solution 3: DP with space compression

```java
// TC: O(n)
// SC: O(1)
class Solution {
    public int rob(int[] nums) {
       int pre = 0, cur = 0;
        for (int i = 0; i < nums.length; i++) {
            int temp = Math.max(pre + nums[i], cur);
            pre = cur;
            cur = temp;
        }
        return cur;
    }
}
```
