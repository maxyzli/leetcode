# Rotate Array

## Solution 1

Brute Force

```java
/**
 * Question   : 189. Rotate Array
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Array
 * Date       : 2021/03/19
 */
class Solution {
    public void rotate(int[] nums, int k) {
        int n = nums.length;

        k = k % n;

        if (k == 0) {
            return;
        }

        int[] res = new int[n];

        int idx = 0;

        for (int i = n - k; i < n; i++) {
            res[idx++] = nums[i];
        }
        for (int i = 0; i < n - k; i++) {
            res[idx++] = nums[i];
        }
        for (int i = 0; i < n; i++) {
            nums[i] = res[i];
        }
    }
}
```

## Solution 2

Reversal

```java
/**
 * Question   : 189. Rotate Array
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Array
 * Date       : 2021/03/19
 */
class Solution {
    public void rotate(int[] nums, int k) {
        int n = nums.length;
        k = k % n;
        reverse(nums, 0, n);
        reverse(nums, 0, k);
        reverse(nums, k, n);
    }

    private void reverse(int[] arr, int fromIndex, int toIndex) {
        int low = fromIndex;
        int high = toIndex - 1;
        while (low < high) {
            int temp = arr[low];
            arr[low] = arr[high];
            arr[high] = temp;
            low++;
            high--;
        }
    }
}
```
