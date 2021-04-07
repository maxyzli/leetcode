# Jump Game

## Solution 1

Greedy

```java
/**
 * Question   : 55. Jump Game
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : array
 */
class Solution {
    public boolean canJump(int[] nums) {
        int n = nums.length;
        int farthest = 0;
        int index = 0;

        while (index < n && farthest >= index) {
            farthest = Math.max(farthest, index + nums[index]);
            index++;
        }

        return index == n;
    }
}
```

## Solution 2

DP

```java
/**
 * Question   : 55. Jump Game
 * Complexity : Time: O(n^2) ; Space: O(n)
 * Topics     : array
 */
class Solution {
    public boolean canJump(int[] nums) {
        if (nums == null || nums.length == 0) {
            return false;
        }

        boolean[] reachable = new boolean[nums.length];
        reachable[0] = true;

        for (int i = 1; i < nums.length; i++) {
            for (int j = 0; j < i; j++) {
                if (!reachable[j]) {
                    continue;
                }
                if (j + nums[j] >= i) {
                    reachable[i] = true;
                }
            }
            if (reachable[i] != true) {
                return false;
            }
        }

        return true;
    }
}
```
