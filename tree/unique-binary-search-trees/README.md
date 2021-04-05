# Unique Binary Search Trees

## Solution 1

Recursion (Time Limit Exceeded)

```jsx
/**
 * Question   : 96. Unique Binary Search Trees
 * Complexity : Time: O(exp) ; Space: O(n)
 * Topics     : Tree
 */
public class Solution {
    public int numTrees(int n) {
        if (n == 0) {
            return 1;
        }

        int ways = 0;

        for (int i = 1; i <= n; i++) {
            int left = numTrees(i - 1);
            int right = numTrees(n - i);
            ways += left * right;
        }

        return ways;
    }
}
```

## Solution 2

Top Down DP

```jsx
/**
 * Question   : 96. Unique Binary Search Trees
 * Topics     : Tree
 * Complexity : Time: O(n^2) ; Space: O(n)
 */
class Solution {
    int[] memo;

    public int numTrees(int n) {
        memo = new int[n + 1];
        memo[0] = 1;
        return numTreesUtil(n);
    }

    private int numTreesUtil(int n) {
        if (memo[n] != 0) {
            return memo[n];
        }

        int count = 0;
        for (int i = 1; i <= n; i++) {
            int left = numTreesUtil(i - 1);
            int right = numTreesUtil(n - i);
            count += left * right;
        }

        memo[n] = count;

        return memo[n];
    }
}
```

## Solution 3

Bottom Up DP

```jsx
/**
 * Question   : 96. Unique Binary Search Trees
 * Topics     : Tree
 * Complexity : Time: O(n^2) ; Space: O(n)
 */
class Solution {
    public int numTrees(int n) {
        int[] memo = new int[n + 1];
        memo[0] = 1;
        memo[1] = 1;

        for (int numberOfNode = 2; numberOfNode <= n; numberOfNode++) {
            for (int rootIdx = 1; rootIdx <= numberOfNode; rootIdx++) {
                memo[numberOfNode] += memo[rootIdx - 1] * memo[numberOfNode - rootIdx];
            }
        }

        return memo[n];
    }
}
```
