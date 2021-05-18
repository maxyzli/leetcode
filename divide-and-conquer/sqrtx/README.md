# Sqrt(x)

## Solution 1

```java
/**
 * Question   : 69. Sqrt(x)
 * Complexity : Time: O(log(n)) ; Space: O(1)
 * Topics     : Divide and Conquer
 */
class Solution {
    public int mySqrt(int x) {
        if (x <= 1) {
            return x;
        }

        int low = 0;
        int high = x;

        int res = 0;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (mid == x / mid) {
                return mid;
            } else if (mid > x / mid) {
                high = mid - 1;
            } else {
                res = mid;
                low = mid + 1;
            }
        }

        return res;
    }
}
```
