# Rotate Array

## Solution 1

Temp Array

```java
/**
 * Question   : 189. Rotate Array
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Array
 */
class Solution {
    public void rotate(int[] nums, int k) {
        int n = nums.length;

        k = k % n;

        if (k == 0) {
            return;
        }

        int[] temp = new int[n];

        for (int i = 0; i < nums.length; i++) {
            int index = (i + k) % n;
            temp[index] = nums[i];
        }

        for (int i = 0; i < nums.length; i++) {
            nums[i] = temp[i];
        }
    }
}
```

## Solution 2

```java
/**
 * Question   : 189. Rotate Array
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public void rotate(int[] nums, int k) {
        if (nums == null || nums.length == 0) {
            return;
        }

        int n = nums.length;
        k = k % n;
        int count = 0;
        int start = 0;

        while (count < n) {
            int curr = start;
            int preVal = nums[curr];

            do {
                int next = (curr + k) % n;

                int temp = nums[next];
                nums[next] = preVal;
                preVal = temp;

                curr = next;
                count++;
            } while (curr != start);

            start++;
        }
    }
}
```

## Solution 3

3 Reverse Thinking

```java
/**
 * Question   : 189. Rotate Array
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Array
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