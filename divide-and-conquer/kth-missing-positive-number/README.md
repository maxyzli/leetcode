# Kth Missing Positive Number

## Solution 1

```java
/**
 * Question   : 1539. Kth Missing Positive Number
 * Complexity : Time: O(log(n)) ; Space: O(1)
 * Topics     : Divide and Conquer
 */
class Solution {
    public int findKthPositive(int[] arr, int k) {
        if (arr[0] > k) {
            return k;
        }

        int low = 0;
        int high = arr.length;

        while (low < high) {
            int mid = low + (high - low) / 2;
            int numberOfMissing = arr[mid] - mid - 1;

            if (numberOfMissing < k) {
                low = mid + 1;
            } else {
                high = mid;
            }
        }

        int numberOfMissing = arr[low - 1] - (low - 1) - 1;
        return arr[low - 1] + (k - numberOfMissing);
    }
}
```
