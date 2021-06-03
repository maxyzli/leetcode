# Minimum Size Subarray Sum

## Solution 1

```java
/**
 * Question   : 209. Minimum Size Subarray Sum
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Sliding Window
 */
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int minLen = Integer.MAX_VALUE;
        int left = 0;
        int right = 0;
        int currSum = 0;

        while (right < nums.length) {
            currSum += nums[right++];

            while (currSum >= target) {
                minLen = Math.min(minLen, right - left);
                currSum -= nums[left++];
            }
        }

        return minLen == Integer.MAX_VALUE ? 0 : minLen;
    }
}
```
