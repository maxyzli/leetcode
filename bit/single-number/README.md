# Single Number

## Solution 1

```java
/**
 * Question   : 136. Single Number
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Bit
 */
class Solution {
    public int singleNumber(int[] nums) {
        int res = nums[0];
        for (int i = 1; i < nums.length; i++) {
            res ^= nums[i];
        }
        return res;
    }
}
```
