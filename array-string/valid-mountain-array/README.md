# Valid Mountain Array

## Solution 1

```java
/**
 * Question   : 941. Valid Mountain Array
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public boolean validMountainArray(int[] arr) {
        if (arr == null || arr.length < 3) {
            return false;
        }

        int i = 1;
        for (; i < arr.length; i++) {
            if (arr[i - 1] >= arr[i]) {
                break;
            }
        }

        // Decreasing.
        if (i == 1) {
            return false;
        }
        // all increasing.
        if (i == arr.length) {
            return false;
        }

        // Check decreasing.
        for (; i < arr.length; i++) {
            if (arr[i - 1] <= arr[i]) {
                return false;
            }
        }

        return true;
    }
}
```