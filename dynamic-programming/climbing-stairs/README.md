# Climbing Stairs

## Solution 1: DP

```java
// TC: O(n)
// SC: O(n)
class Solution {
    public int climbStairs(int n) {
        int[] mem = new int[n + 1];
        mem[0] = 1;
        mem[1] = 1;

        for (int i = 2; i <= n; i++) {
            mem[i] = mem[i - 2] + mem[i - 1];
        }

        return mem[n];
    }
}
```
