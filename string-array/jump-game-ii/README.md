# Jump Game II

## Solution 1

DP

```java
/**
 * Question   : 45. Jump Game II
 * Complexity : Time: O(n^2) ; Space: O(n)
 * Topics     : DP
 */
class Solution {
    public int jump(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int[] memo = new int[nums.length];
        Arrays.fill(memo, Integer.MAX_VALUE);
        memo[0] = 0;

        for (int i = 1; i < nums.length; i++) {
            for (int j = 0; j < i; j++) {
                // Check if we can jump from j to i.
                if (j + nums[j] >= i) {
                    memo[i] = Math.min(memo[i], 1 + memo[j]);
                }
            }
        }

        return memo[nums.length - 1];
    }
}
```

## Solution 2

Greedy

```java
/**
 * Question   : 55. Jump Game
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : array
 */
class Solution {
    public int jump(int[] nums) {
        int farthestNextJump = 0;
        int farthestCurrJump = 0;
        int step = 0;

        for (int i = 0; i < nums.length - 1; i++) {
            farthestNextJump = Math.max(farthestNextJump, i + nums[i]);
            if (i == farthestCurrJump) {
                step++;
                farthestCurrJump = farthestNextJump;
            }
        }

        return step;
    }
}
```
