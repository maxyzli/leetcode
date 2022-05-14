# Search in Rotated Sorted Array

## Solution 1

```java
// TC: O(log(n)
// SC: O(1)
class Solution {
    public int search(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return -1;
        }

        int lo = 0;
        int hi = nums.length - 1;

        while (lo <= hi) {
            int mid = lo + (hi - lo) / 2;

            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] > nums[hi]) { // left sorted
                if (nums[lo] <= target && target < nums[lo]) {
                    hi = mid - 1;
                } else {
                    lo = mid + 1;
                }
            } else { // right sorted
                if (nums[mid] < target && target <= nums[hi]) {
                    lo = mid + 1;
                } else {
                    hi = mid - 1;
                }
            }
        }

        return -1;
    }
}
```

## Solution 2

Compare left with mid

```java
/**
 * Question   : 33. Search in Rotated Sorted Array
 * Complexity : Time: O(log(n)) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public int search(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return -1;
        }

        int low = 0;
        int high = nums.length - 1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (nums[mid] == target) {
                return mid;
            } else if (nums[low] <= nums[mid]) { // left sorted
                // If target is between low and mid -> search left part.
                if (nums[low] <= target && target < nums[mid]) {
                    high = mid - 1;
                } else {
                    low = mid + 1;
                }
            } else { // right sorted
                // If target is between mid and high -> search right part.
                if (nums[mid] < target && target <= nums[high]) {
                    low = mid + 1;
                } else {
                    high = mid - 1;
                }
            }
        }

        return -1;
    }
}
```
