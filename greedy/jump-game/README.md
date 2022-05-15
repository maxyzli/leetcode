# Jump Game

## Solution 1: DP

```java
// TC: O(n^2)
// SC: O(n)
class Solution {
    public boolean canJump(int[] nums) {
        int n = nums.length;

        boolean[] dp = new boolean[n];
        dp[0] = true;

        for (int i = 0; i < n; i++) {
            if (!dp[i]) {
                continue;
            }
            for (int step = 1; step <= nums[i]; step++) {
                if (i + step >= n) {
                    return true;
                }
                dp[i + step] = true;
            }
        }

        return dp[n - 1];
    }
}
```

## Solution 2: Greedy

```java
// TC: O(n)
// SC: O(n)
class Solution {
    public boolean canJump(int[] nums) {
        int n = nums.length;

        int farthest = 0;

        for (int i = 0; i < n; i++) {
            // Unreachable.
            if (farthest < i) {
                return false;
            }

            farthest = Math.max(farthest, i + nums[i]);

            if (farthest >= n - 1) {
                return true;
            }
        }

        return false;
    }
}
```
