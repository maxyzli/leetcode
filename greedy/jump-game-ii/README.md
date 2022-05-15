# Jump Game II

## Solution 1: DP

```java
// TC: O(n^2)
// SC: O(n)
class Solution {
    public int jump(int[] nums) {
        int n = nums.length;

        int[] dp = new int[n];
        Arrays.fill(dp, Integer.MAX_VALUE);
        dp[0] = 0;

        for (int i = 0; i < n; i++) {
            if (dp[i] == Integer.MAX_VALUE) {
                continue;
            }
            for (int step = 1; step <= nums[i]; step++) {
                int dest = Math.min(i + step , n - 1);
                dp[dest] = Math.min(dp[dest],  dp[i] + 1);
            }
        }

        return dp[n - 1];
    }
}
```

## Solution 2: Greedy

```java
// TC: O(n)
// SC: O(1)
class Solution {
    public int jump(int[] nums) {
        if (nums.length <= 1) {
            return 0;
        }

        int step = 0;
        int currFarthest = 0;
        int nextFarthest = 0;

        for (int i = 0; i < nums.length; i++) {
            nextFarthest = Math.max(nextFarthest, i + nums[i]);
            if (i == currFarthest) {
                step++;
                if (nextFarthest >= nums.length - 1) {
                    return step;
                }
                currFarthest = nextFarthest;
            }
        }

        return step;
    }
}
```
