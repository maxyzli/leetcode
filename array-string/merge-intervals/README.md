# Merge Intervals

## Solution 1

Assume integers are unique.

```java
/**
 * Question   : 35. Search Insert Position
 * Complexity : Time: O(log(n)) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public int searchInsert(int[] nums, int target) {
        int low = 0;
        int high = nums.length - 1;

        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] > target) {
                high = mid - 1;
            } else {
                low = mid + 1;
            }
        }

        return low;
    }
}
```

## Solution 2

Assume integers are not unique.

```java
/**
 * Question   : 35. Search Insert Position
 * Complexity : Time: O(log(n)) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public int searchInsert(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int low = 0;
        int high = nums.length;

        // Find the first value which is equal or bigger than the target.
        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (nums[mid] == target) {
                if (mid == 0 || nums[mid - 1] != target) {
                    return mid;
                }
                high = mid - 1;
            } else if (nums[mid] < target) {
                // nums[mid] is smaller than the target.
                // If the next value is bigger than the target, we should insert target at mid + 1 position.
                // => num[mid] < target < num[mid + 1]
                if (mid == nums.length - 1 || target < nums[mid + 1]) {
                    return mid + 1;
                }
                low = mid + 1;
            } else {
                // nums[mid] is bigger than the target.
                // If the previous value is smaller than the target, we should insert target at mid position.
                // => num[mid - 1] < target < num[mid]
                if (mid == 0 || nums[mid - 1] < target) {
                    return mid;
                }
                high = mid - 1;
            }
        }

        return -1;
    }
}
```
