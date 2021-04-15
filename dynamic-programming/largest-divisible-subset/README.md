# Largest Divisible Subset

## Solution 1

DP

```java
/**
 * Question   : 368. Largest Divisible Subset
 * Topics     : DP
 * Complexity : Time: O(n^2) ; Space: O(n)
 */
class Solution {
    public List<Integer> largestDivisibleSubset(int[] nums) {
        if (nums == null || nums.length == 0) {
            return new ArrayList<>();
        }

        Arrays.sort(nums);

        int n = nums.length;

        int[] memo = new int[n];

        for (int i = 0; i < n; i++) {
            memo[i] = 1;
        }

        int maxLen = 1;
        // Longest Increasing Subsequence
        for (int j = 1; j < memo.length; j++) {
            for (int i = 0; i < j; i++) {
                if (nums[j] % nums[i] == 0) {
                    memo[j] = Math.max(memo[j], memo[i] + 1);
                    maxLen = Math.max(maxLen, memo[j]);
                }
            }
        }

        List<Integer> list = new ArrayList<>();

        int len = maxLen;
        int prev = -1;
        for (int i = n - 1; i >= 0; i--) {
            if (memo[i] == len && (prev == -1 || prev % nums[i] == 0)) {
                list.add(nums[i]);
                prev = nums[i];
                len--;
            }
        }

        return list;
    }
}
```
