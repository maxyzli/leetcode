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
        int currSum = 0;

        for (int i = 0; i < k; i++) {
            currSum += nums[i];
        }

        double res = (1.0 * currSum) / k;

        for (int i = k; i < nums.length; i++) {
            currSum -= nums[i - k];
            currSum += nums[i];
            res = Math.max(res, (1.0 * currSum) / k);
        }

        return res;
    }
}
```
