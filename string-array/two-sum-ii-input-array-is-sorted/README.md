# Two Sum II - Input array is sorted

## Solution 1

Two Pointer

```java
/**
 * Question   : 167. Two Sum II - Input array is sorted
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        if (numbers == null || numbers.length == 0) {
            return new int[]{};
        }

        int left = 0, right = numbers.length - 1;

        while (left < right) {
            if (numbers[left] + numbers[right] == target) {
                return new int[]{left + 1, right + 1};
            } else if (numbers[left] + numbers[right] > target) {
                right--;
            } else {
                left++;
            }
        }

        return new int[]{};
    }
}
```

## Solution 2

Binary Search

```java
/**
 * Question   : 167. Two Sum II - Input array is sorted
 * Complexity : Time: O(log(n)) ; Space: O(1)
 * Topics     : Array
 */
public class Solution {
    public int[] twoSum(int[] arr, int target) {
        if (arr == null || arr.length == 0) {
            return new int[]{};
        }

        int low = 0;
        int high = arr.length - 1;

        while (low <= high) {
            if (arr[low] + arr[high] == target) {
                return new int[]{low + 1, high + 1};
            } else if (arr[low] + arr[high] < target) {
                low = findClosest(arr, low + 1, high - 1, target - arr[high]);
            } else {
                high = findClosest(arr, low + 1, high - 1, target - arr[low]);
            }
        }

        return new int[]{};
    }

    private int findClosest(int[] arr, int low, int high, int target) {
        int diff = Integer.MAX_VALUE;
        int closestIdx = low;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (Math.abs(arr[mid] - target) <= diff) {
                closestIdx = mid;
                diff = Math.abs(arr[mid] - target);
            }

            if (arr[mid] == target) {
                return mid;
            } else if (arr[mid] < target) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }

        return closestIdx;
    }
}
```
