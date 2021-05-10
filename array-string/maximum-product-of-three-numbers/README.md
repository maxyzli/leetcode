# Maximum Product of Three Numbers

## Solution 1

```java
/**
 * Question   : 628. Maximum Product of Three Numbers
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public int maximumProduct(int[] nums) {
        int min1 = Integer.MAX_VALUE;
        int min2 = Integer.MAX_VALUE;
        int max1 = Integer.MIN_VALUE;
        int max2 = Integer.MIN_VALUE;
        int max3 = Integer.MIN_VALUE;

        for (int i = 0; i < nums.length; i++) {
            int num = nums[i];

            if (min1 > num) {
                min2 = min1;
                min1 = num;
            } else if (min2 > num) {
                min2 = num;
            }

            if (num > max1) {
                max3 = max2;
                max2 = max1;
                max1 = num;
            } else if (num > max2) {
                max3 = max2;
                max2 = num;
            } else if (num > max3) {
                max3 = num;
            }
        }

        return Math.max(max1 * max2 * max3, max1 * min1 * min2);
    }
}
```
