# Max Consecutive Ones

## Solution 1

```java
/**
 * Question   : 485. Max Consecutive Ones
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int curr = 0;
        int max = 0;
        
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == 0) {
                curr = 0;
            } else {
                curr++;
                max = Math.max(max, curr);
            }
        }
        
        return max;
    }
}
```
