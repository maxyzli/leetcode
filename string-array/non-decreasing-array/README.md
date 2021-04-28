# Non-decreasing Array

## Solution 1

```java
/**
 * Question   : 665. Non-decreasing Array
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public boolean checkPossibility(int[] nums) {
        if (nums == null || nums.length == 0) {
            return true;
        }

        int opportunities = 1;

        for (int i = 1; i < nums.length; i++) {
            // previous number is bigger than current number.
            if (nums[i - 1] > nums[i]) {
                if (opportunities == 0) {
                    return false;
                }

                if (i == 1 || nums[i - 2] <= nums[i]) {
                    nums[i - 1] = nums[i];
                } else { // nums[i - 2] > nums[i]
                    nums[i] = nums[i - 1];
                }

                opportunities--;
            }
        }

        return true;
    }
}
```