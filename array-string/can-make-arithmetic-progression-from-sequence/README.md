# Can Make Arithmetic Progression From Sequence

## Solution 1

```java
/**
 * Question   : 1502. Can Make Arithmetic Progression From Sequence
 * Complexity : Time: O(nlog(n)) ; Space: O(n)
 * Topics     : Array
 */
class Solution {
    public boolean canMakeArithmeticProgression(int[] arr) {
        Arrays.sort(arr);

        int progression = 0;
        for (int i = 1; i < arr.length; i++) {
            int diff = arr[i] - arr[i - 1];

            if (i == 1) {
                progression = diff;
                continue;
            }

            if (progression != diff) {
                return false;
            }
        }

        return true;
    }
}
```
