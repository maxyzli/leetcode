# Count Inversions in an array

## Solution 1

Brute Force

```java
public class Solution {
    public int reversePairs(int[] nums) {
        int count = 0;
        int len = nums.length;
        for (int i = 0; i < len - 1; i++) {
            for (int j = i + 1; j < len; j++) {
                if (nums[i] > nums[j]) {
                    count++;
                }
            }
        }
        return count;
    }
}
```

## Solution 2

Merge Sort

```java
/**
 * Question   : Count Inversions in an array
 * Complexity : Time: O(nlog(n)) ; Space: O(1)
 * Topics     : Divide and Conquer
 */
public class Solution {
    public int reversePairs(int[] arr) {
        if (arr == null || arr.length == 0) {
            return 0;
        }
        return mergeSort(arr, 0, arr.length - 1);
    }

    public int mergeSort(int[] arr, int low, int high) {
        if (low == high) {
            return 0;
        }

        int mid = low + (high - low) / 2;

        int leftCount = mergeSort(arr, low, mid);
        int rightCount = mergeSort(arr, mid + 1, high);

        return leftCount + rightCount + merge(arr, low, mid, high);
    }

    public int merge(int[] arr, int low, int mid, int high) {
        int[] merged = new int[high - low + 1];

        int i = low, j = mid + 1, k = 0;

        int inversion = 0;

        while (i <= mid && j <= high) {
            if (arr[i] <= arr[j]) {
                merged[k++] = arr[i++];
            } else {
                merged[k++] = arr[j++];
                inversion += mid - i + 1;
            }
        }
        while (i <= mid) {
            merged[k++] = arr[i++];
        }
        while (j <= high) {
            merged[k++] = arr[j++];
        }

        k = 0;
        for (; k < merged.length; k++) {
            arr[low + k] = merged[k];
        }

        return inversion;
    }
}
```
