# Climbing Stairs

## Solution 1

DFS (Time Limit Exceeded)

```java
/**
 * Question   : 70. Climbing Stairs
 * Complexity : Time: O(2^n) ; Space: O(n)
 * Topics     : DP
 */
class Solution {
    int ways = 0;

    public int climbStairs(int n) {
        ways = 0;
        dfs(n, 0);
        return ways;
    }

    private void dfs(int n, int level) {
        if (level > n) {
            return;
        }
        if (level == n) {
            ways++;
            return;
        }

        for (int step = 1; step <= 2; step++) {
            dfs(n, level + step);
        }
    }
}
```

## Solution 2

DFS (Time Limit Exceeded)

```java
/**
 * Question   : 70. Climbing Stairs
 * Complexity : Time: O(2^n) ; Space: O(n)
 * Topics     : DP
 */
class Solution {
    public int climbStairs(int n) {
        return dfs(n, 0);
    }

    private int dfs(int n, int level) {
        if (level > n) {
            return 0;
        }
        if (level == n) {
            return 1;
        }

        int count = 0;
        for (int step = 1; step <= 2; step++) {
            count += dfs(n, level + step);
        }

        return count;
    }
}
```

## Solution 3

Top-Down DP

```java
/**
 * Question   : 70. Climbing Stairs
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : DP
 */
class Solution {
    int[] memo;

    public int climbStairs(int n) {
        memo = new int[n];
        dfs(n, 0);
        return memo[0];
    }

    private int dfs(int n, int level) {
        if (level > n) {
            return 0;
        }
        if (level == n) {
            return 1;
        }

        if (memo[level] != 0) {
            return memo[level];
        }

        int count = 0;
        for (int step = 1; step <= 2; step++) {
            count += dfs(n, level + step);
        }

        memo[level] = count;

        return memo[level];
    }
}
```

## Solution 4

Bottom-Up DP

```java
/**
 * Question   : 70. Climbing Stairs
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : DP
 */
class Solution {
    public int climbStairs(int n) {
        int[] memo = new int[n + 1];
        memo[0] = 1;
        memo[1] = 1;

        for (int floor = 2; floor <= n; floor++) {
            memo[floor] = memo[floor - 1] + memo[floor - 2];
        }

        return memo[n];
    }
}
```
