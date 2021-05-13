# Jump Game II

## Solution 1

DFS

```java
/**
 * Question   : 45. Jump Game II
 * Complexity : Time: O(n!) ; Space: O(n)
 * Topics     : DP
 */
class Solution {
    int min = Integer.MAX_VALUE;

    public int jump(int[] nums) {
        min = Integer.MAX_VALUE;

        int beginIndex = 0;
        dfs(nums, beginIndex, 0);

        return min;
    }

    private void dfs(int[] nums, int beginIndex, int numberOfJump) {
        if (beginIndex == nums.length - 1) {
            min = Math.min(min, numberOfJump);
            return;
        }
        if (beginIndex >= nums.length) {
            return;
        }
        
        for (int distance = 1; distance <= nums[beginIndex]; distance++) {
            dfs(nums, beginIndex + distance, numberOfJump + 1);
        }
    }
}
```

## Solution 2

DFS

```java
/**
 * Question   : 45. Jump Game II
 * Complexity : Time: O(n!) ; Space: O(n)
 * Topics     : DP
 */
class Solution {
    public int jump(int[] nums) {
        int beginIndex = 0;
        return dfs(nums, beginIndex);
    }

    private int dfs(int[] nums, int beginIndex) {
        if (beginIndex == nums.length - 1) {
            return 0;
        }
        if (beginIndex >= nums.length) {
            return Integer.MAX_VALUE;
        }

        int min = Integer.MAX_VALUE;
        for (int distance = 1; distance <= nums[beginIndex]; distance++) {
            int numberOfJumps = dfs(nums, beginIndex + distance);
            if (numberOfJumps != Integer.MAX_VALUE) {
                min = Math.min(min, 1 + numberOfJumps);
            }
        }
        
        return min;
    }
}
```

## Solution 3

DFS + Memoization (Top-Down DP)

```java
/**
 * Question   : 45. Jump Game II
 * Complexity : Time: O(n^2) ; Space: O(n)
 * Topics     : DP
 */
class Solution {
    public int jump(int[] nums) {
        if (nums == null || nums.length == 1) {
            return 0;
        }
        
        int[] memo = new int[nums.length];
        Arrays.fill(memo, Integer.MAX_VALUE);
        memo[nums.length - 1] = 0;
        
        dfs(nums, 0, memo);
        
        return memo[0];
    }

    private int dfs(int[] nums, int beginIndex, int[] memo) {
        if (beginIndex == nums.length - 1) {
            return 0;
        }
        if (beginIndex >= nums.length) {
            return Integer.MAX_VALUE;
        }

        if (memo[beginIndex] != Integer.MAX_VALUE) {
            return memo[beginIndex];
        }

        int min = Integer.MAX_VALUE;
        for (int distance = 1; distance <= nums[beginIndex]; distance++) {
            int numberOfJumps = dfs(nums, beginIndex + distance, memo);
            if (numberOfJumps != Integer.MAX_VALUE) {
                min = Math.min(min, 1 + numberOfJumps);
            }
        }

        memo[beginIndex] = min;

        return memo[beginIndex];
    }
}
```

## Solution 4

Iteration + Memoization (Bottom-Up DP)

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

## Solution 5

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
