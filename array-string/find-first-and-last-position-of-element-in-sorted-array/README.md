# Find First and Last Position of Element in Sorted Array

## Solution 1

```java
/**
 * Question   : Find First and Last Position of Element in Sorted Array
 * Complexity : Time: O(log(n)) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public int[] searchRange(int[] array, int target) {
        return new int[]{findStartPosition(array, target), findEndPosition(array, target)};
    }

    private static int findStartPosition(int[] array, int target) {
        int low = 0, high = array.length - 1;

        int startIdx = -1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (array[mid] == target) {
                startIdx = mid;
                high = mid - 1;
            } else if (array[mid] < target) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }

        return startIdx;
    }

    private static int findEndPosition(int[] array, int target) {
        int low = 0, high = array.length - 1;

        int endIdx = -1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (array[mid] == target) {
                endIdx = mid;
                low = mid + 1;
            } else if (array[mid] < target) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }

        return endIdx;
    }
}
```

## Solution 2

```java
/**
 * Question   : Find First and Last Position of Element in Sorted Array
 * Complexity : Time: O(log(n)) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public int[] searchRange(int[] array, int target) {
        return new int[]{findStartPosition(array, target), findEndPosition(array, target)};
    }

    private static int findStartPosition(int[] array, int target) {
        int low = 0, high = array.length - 1;

        int startIdx = -1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (array[mid] == target) {
                if (mid == 0) {
                    return mid;
                }
                // Check if the previous value is the same as the mid value.
                if (array[mid - 1] == array[mid]) {
                    high = mid - 1;
                } else {
                    return mid;
                }
            } else if (array[mid] < target) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }

        return startIdx;
    }

    private static int findEndPosition(int[] array, int target) {
        int low = 0, high = array.length - 1;

        int endIdx = -1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (array[mid] == target) {
                if (mid == array.length - 1) {
                    return mid;
                }
                // Check if the next value is the same as the mid value.
                if (array[mid] == array[mid + 1]) {
                    low = mid + 1;
                } else {
                    return mid;
                }
            } else if (array[mid] < target) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }

        return endIdx;
    }
}
```
