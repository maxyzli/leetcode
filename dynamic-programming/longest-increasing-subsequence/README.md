# Longest Increasing Subsequence

## Solution 1

DP

```java
/**
 * Question   : 300. Longest Increasing Subsequence
 * Complexity : Time: O(n^2) ; Space: O(n)
 * Topics     : DP
 */
public class Solution {
    public int lengthOfLIS(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int[] memo = new int[nums.length];

        for (int i = 0; i < nums.length; i++) {
            memo[i] = 1;
        }

        int longest = 1;

        for (int j = 1; j < nums.length; j++) {
            for (int i = 0; i < j; i++) {
                if (nums[i] < nums[j]) {
                    memo[j] = Math.max(memo[j], memo[i] + 1);
                    longest = Math.max(longest, memo[j]);
                }
            }
        }

        return longest;
    }
}
```
