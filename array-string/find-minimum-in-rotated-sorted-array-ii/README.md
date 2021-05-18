# Find Minimum in Rotated Sorted Array II

## Solution 1

```java
/**
 * Question   : 153. Find Minimum in Rotated Sorted Array
 * Complexity : Time: O(log(n)) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public int findMin(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int low = 0;
        int high = nums.length - 1;
        int min = Integer.MAX_VALUE;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            min = Math.min(min, nums[mid]);

            // 4 4 4 0 4 4
            // l   m     r
            if (nums[mid] == nums[high]) {
                high--;
            } else if (nums[mid] < nums[high]) {
                high = mid - 1;
            } else {
                low = mid + 1;
            }
        }

        return min;
    }
}
```
