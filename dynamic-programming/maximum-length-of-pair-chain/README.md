# Maximum Length of Pair Chain

## Solution 1

DP

```java
/**
 * Question   : 646. Maximum Length of Pair Chain
 * Complexity : Time: O(n^2) ; Space: O(n)
 * Topics     : DP
 */
public class Solution {
    public int findLongestChain(int[][] pairs) {
        Arrays.sort(pairs, (a, b) -> {
            if (a != b) {
                return a[0] - b[0];
            }
            return a[1] - b[1];
        });

        int n = pairs.length;

        // dp[i] = longest pair chain for index i.
        int[] dp = new int[n];
        Arrays.fill(dp, 1);

        for (int i = 1; i < n; i++) {
            for (int j = 0; j < i; j++) {
                int[] a = pairs[i];
                int[] b = pairs[j];
                if (b[1] < a[0]) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
            }
        }

        return dp[n - 1];
    }
}
```
