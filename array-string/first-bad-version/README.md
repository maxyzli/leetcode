# First Bad Version

## Solution 1

```java
/**
 * Question   : 278. First Bad Version
 * Complexity : Time: O(log(n)) ; Space: O(1)
 * Topics     : Array
 */
public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int low = 1;
        int high = n;

        int firstIndex = low;

        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (isBadVersion(mid)) {
                firstIndex = mid;
                high = mid - 1;
            } else {
               low = mid + 1;
            }
        }

        return firstIndex;
    }
}
```
