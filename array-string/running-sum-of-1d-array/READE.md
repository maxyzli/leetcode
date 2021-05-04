# Running Sum of 1d Array

## Solution 1

```java
/**
 * Question   : 1480. Running Sum of 1d Array
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public int[] runningSum(int[] nums) {
        if (nums == null || nums.length == 0) {
           return nums;
        }
        
        int currSum = 0;
        
        for (int i = 0; i < nums.length; i++) {
            currSum += nums[i];
            nums[i] = currSum;
        }
        
        return nums;
    }
}
```