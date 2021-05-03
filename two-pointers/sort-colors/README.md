# Sort Colors

## Solution 1

Counting Sort

```java
/**
 * Question   : 75. Sort Colors
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : array
 */
class Solution {
    public void sortColors(int[] nums) {
        if (nums == null || nums.length == 0) {
            return;
        }

        int[] counts = new int[3];

        for (int i = 0; i < nums.length; i++) {
            counts[nums[i]]++;
        }

        for (int i = 1; i < counts.length; i++) {
            counts[i] += counts[i - 1];
        }

        int[] output = new int[nums.length];
        for (int i = nums.length - 1; i >= 0; i--) {
            int index = counts[nums[i]] - 1;
            output[index] = nums[i];
            counts[nums[i]]--;
        }

        for (int i = 0; i < output.length; i++) {
            nums[i] = output[i];
        }
    }
}
```

## Solution 2

3 pointers

```java
/**
 * Question   : 75. Sort Colors
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : array
 */
class Solution {
    public void sortColors(int[] arr) {
        if (arr == null || arr.length == 0) {
            return;
        }

        int i = 0;
        int j = 0;
        int k = arr.length - 1;

        while (j <= k) {
            if (arr[j] == 0) {
                swap(arr, i, j);
                i++;
                j++;
            } else if (arr[j] == 1) {
                j++;
            } else if (arr[j] == 2) {
                swap(arr, j, k);
                k--;
            }
        }
    }

    private void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
}
```
