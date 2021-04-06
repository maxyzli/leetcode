# Find Peak Element

## Solution 1

```java
/**
 * Question   : Find a peak element
 * Complexity : Time: O(log(n)) ; Space: O(1)
 * Topics     : Array
 */
public class Solution {
    public int findPeakElement(int[] arr) {
        if (arr == null || arr.length == 0) {
            return Integer.MIN_VALUE;
        }

        int low = 0, high = arr.length - 1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if ((mid == 0 || arr[mid - 1] < arr[mid]) && (mid == arr.length - 1 || arr[mid] > arr[mid + 1])) {
                return mid;
            } else if (mid != 0 && arr[mid - 1] > arr[mid]) {
                high = mid - 1;
            } else {
                low = mid + 1;
            }
        }

        return Integer.MIN_VALUE;
    }
}
```
