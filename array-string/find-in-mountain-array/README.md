# Find in Mountain Array

## Solution 1

```java
/**
 * Question   : 1095. Find in Mountain Array
 * Complexity : Time: O(log(n)) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public int findInMountainArray(int target, MountainArray mountainArr) {
        int peakIdx = findPeakIndex(mountainArr);

        int idx = binarySearch(target, mountainArr, 0, peakIdx);
        if (idx != -1) {
            return idx;
        }

        return revBinarySearch(target, mountainArr, peakIdx + 1, mountainArr.length() - 1);
    }

    private int findPeakIndex(MountainArray mountainArr) {
        int n = mountainArr.length();

        int low = 0;
        int high = n - 1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if ((mid == 0 || mountainArr.get(mid - 1) < mountainArr.get(mid)) && (mid == n - 1 || (mountainArr.get(mid) > mountainArr.get(mid + 1)))) {
                return mid;
            } else if (mountainArr.get(mid) < mountainArr.get(mid + 1)) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }

        return -1;
    }

    private int binarySearch(int target, MountainArray mountainArr, int low, int high) {
        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (mountainArr.get(mid) == target) {
                return mid;
            } else if (mountainArr.get(mid) > target) {
                high = mid - 1;
            } else {
                low = mid + 1;
            }
        }

        return -1;
    }

    private int revBinarySearch(int target, MountainArray mountainArr, int low, int high) {
        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (mountainArr.get(mid) == target) {
                return mid;
            } else if (mountainArr.get(mid) > target) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }

        return -1;
    }
}
```
