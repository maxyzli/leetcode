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

        int left = 0;
        int right = 0;

        while (right < k) {
            currSum += nums[right++];
        }

        double res = (1.0 * currSum) / k;

        while (right < nums.length) {
            currSum += nums[right++];
            currSum -= nums[left++];
            res = Math.max(res, (1.0 * currSum) / k);
        }

        return res;
    }
}
```
