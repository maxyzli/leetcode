# Maximum Average Subarray I

## Solution 1

```java
/**
 * Question   : 643. Maximum Average Subarray I
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Sliding Window
 */
public class Solution {
    public double findMaxAverage(int[] nums, int k) {
        int left = 0;
        int right = 0;
        int currSum = 0;

        double res = Integer.MIN_VALUE;

        while (right < nums.length) {
            currSum += nums[right++];
            if (right - left == k) {
                res = Math.max(res, (1.0 * currSum) / k);
                currSum -= nums[left++];
            }
        }

        return res;
    }
}
```
