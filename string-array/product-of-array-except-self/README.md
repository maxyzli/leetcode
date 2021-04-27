# Product of Array Except Self

## Solution 1

```java
/**
 * Question   : 1480. Running Sum of 1d Array
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Array
 */
class Solution {
    public int[] productExceptSelf(int[] nums) {
        if (nums == null || nums.length == 0) {
            return nums;
        }

        int n = nums.length;

        int[] left = new int[n];
        left[0] = 1;

        for (int i = 1; i < n; i++) {
           left[i] = nums[i - 1] * left[i - 1];
        }

        int[] right = new int[n];
        right[n - 1] = 1;

        for (int i = n - 2; i >= 0; i--) {
            right[i] = nums[i + 1] * right[i + 1];
        }

        for (int i = 0; i < n; i++) {
            nums[i] = left[i] * right[i];
        }
        
        return nums;
    }
}
```

## Solution 2

O(1) Space

```java
/**
 * Question   : 1480. Running Sum of 1d Array
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public int[] productExceptSelf(int[] array) {
        int N = array.length;

        int[] output = new int[N];

        int leftProduct = 1;
        for (int i = 0; i < N; i++) {
            output[i] = leftProduct;
            leftProduct *= array[i];
        }

        int rightProduct = 1;
        for (int i = N - 1; i >= 0; i--) {
            output[i] *= rightProduct;
            rightProduct *= array[i];
        }

        return output;
    }
}
```