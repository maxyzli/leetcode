# Maximum Subarray

## Solution 1

DFS (Calculate the Result at Calling Phase)

```java
/**
 * Question   : 53. Maximum Subarray
 * Topics     : DP
 * Complexity : Time: O(n^2) ; Space: O(n)
 */
class Solution {
    int maxSum;

    public int maxSubArray(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        maxSum = Integer.MIN_VALUE;
        for (int i = 0; i < nums.length; i++) {
            maxSubArrayUtil(nums, i + 1, nums[i]);
        }
        return maxSum;
    }

    private void maxSubArrayUtil(int[] nums, int i, int sum) {
        maxSum = Math.max(maxSum, sum);
        if (i == nums.length) {
            return;
        }
        int nextSum = sum + nums[i];
        maxSubArrayUtil(nums, i + 1, nextSum);
    }
}
```

## Solution 2

DFS (Calculate the Result at Returning Phase)

```java
/**
 * Question   : 53. Maximum Subarray
 * Topics     : DP
 * Complexity : Time: O(n^2) ; Space: O(n)
 */
class Solution {
    public int maxSubArray(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int max = Integer.MIN_VALUE;

        for (int i = 0; i < nums.length; i++) {
            max = Math.max(max, maxSubArrayUtil(nums, i));
        }

        return max;
    }

    private int maxSubArrayUtil(int[] nums, int i) {
        if (i == nums.length - 1) {
            return nums[i];
        }

        int maxSum = nums[i];

        int subMaxSum = maxSubArrayUtil(nums, i + 1);

        maxSum = Math.max(maxSum, subMaxSum + maxSum);

        return maxSum;
    }
}
```

## Solution 3

Top-Down DP

```java
/**
 * Question   : 53. Maximum Subarray
 * Topics     : DP
 * Complexity : Time: O(n) ; Space: O(n)
 */
public class Solution {
    int[] memo;

    public int maxSubArray(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int n = nums.length;

				// memo[i]: Max sub-array consider number at i index.
        memo = new int[n];
        Arrays.fill(memo, Integer.MIN_VALUE);

        Integer max = Integer.MIN_VALUE;
        for (int i = 0; i < n; i++) {
            max = Math.max(max, maxSubArrayUtil(nums, i));
        }

        return max;
    }

    private int maxSubArrayUtil(int[] nums, int i) {
        if (i == nums.length - 1) {
            return nums[i];
        }

        if (memo[i] != Integer.MIN_VALUE) {
            return memo[i];
        }

        int maxSum = nums[i];

        int subMaxSum = maxSubArrayUtil(nums, i + 1);

        maxSum = Math.max(maxSum, subMaxSum + maxSum);

        memo[i] = maxSum;

        return memo[i];
    }
}
```

## Solution 4

Bottom-Up DP

```java
/**
 * Question   : Maximum Subarray
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : DP
 */
public class Solution {
    public int maxSubArray(int[] arr) {
        if (arr == null || arr.length == 0) {
            return Integer.MIN_VALUE;
        }

        int[] memo = new int[arr.length];

        memo[0] = arr[0];

        int max = memo[0];

        for (int i = 1; i < arr.length; i++) {
            // We either continue the sub-array or start a new one.
            memo[i] = Math.max(memo[i - 1] + arr[i], arr[i]);
            max = Math.max(max, memo[i]);
        }

        return max;
    }
}
```

## Solution 5

Two Dimensional Array (Memory Limit Exceeded)

```java
/**
 * Question   : Maximum Subarray
 * Complexity : Time: O(n^2) ; Space: O(n^2)
 * Topics     : DP
 */
public class Solution {
    public int maxSubArray(int[] nums) {
        if (nums == null || nums.length == 0) {
            return Integer.MIN_VALUE;
        }

        int n = nums.length;

        int[][] memo = new int[n][n];

        int maxSum = Integer.MIN_VALUE;

        for (int len = 1; len <= n; len++) {
            for (int i = 0; i < n - len + 1; i++) {
                int j = i + len - 1;

                if (i == j) { // len == 1
                    memo[i][j] = nums[i];
                } else if (i == j + 1) { // len == 2
                    memo[i][j] = nums[i] + nums[j];
                } else { // len >= 3
                    memo[i][j] = nums[i] + nums[j] + memo[i + 1][j - 1];
                }

                maxSum = Math.max(maxSum, memo[i][j]);
            }
        }

        return maxSum;
    }
}
```
