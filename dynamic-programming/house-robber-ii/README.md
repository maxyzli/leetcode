# House Robber II

## Solution 1: DP

```java
// TC: O(n)
// SC: O(n)
class Solution {
    public int rob(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        if (nums == null || nums.length == 1) {
            return nums[0];
        }
        if (nums.length == 2) {
            return Math.max(nums[0], nums[1]);
        }

        int resultWithFirst = rob(nums, 0, nums.length - 2);
        int resultWithLast = rob(nums, 1, nums.length - 1);

        return Math.max(resultWithFirst, resultWithLast);
    }

    private int rob(int[] nums, int start, int end) {
        int n = nums.length;

        int[] dp = new int[n];
        dp[start] = nums[start];
        dp[start + 1] = Math.max(nums[start + 1], nums[start]);

        for (int i = start + 2; i <= end; i++) {
            dp[i] = Math.max(dp[i - 2] + nums[i], dp[i - 1]);
        }

        return dp[end];
    }
}
```
