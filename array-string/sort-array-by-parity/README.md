# Sort Array By Parity

## Solution 1

```java
/**
 * Question   : 905. Sort Array By Parity
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public int[] sortArrayByParity(int[] A) {
        if (A == null || A.length == 0) {
            return A;
        }

        int even  = 0;
        int odd = 0;

        // [index 0, even) is even;
        // [even, odd) is odd;
        // [odd, index end] is undetermined.

        while (odd < A.length) {
            if (A[odd] % 2 == 0) {
                swap(A, even++, odd++);
            } else {
                odd++;
            }
        }

        return A;
    }

    private void swap(int[] nums, int p1, int p2) {
        int temp = nums[p1];
        nums[p1] = nums[p2];
        nums[p2] = temp;
    }
}
```

## Solution 2

```java
/**
 * Question   : 905. Sort Array By Parity
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public int[] sortArrayByParity(int[] A) {
        if (A == null || A.length == 0) {
            return A;
        }

        int p1 = 0;
        int p2 = A.length - 1;

        while (p1 < p2) {
            while (p1 < p2 && A[p1] % 2 == 0) {
                p1++;
            }
            while (p1 < p2 && A[p2] % 2 != 0) {
                p2--;
            }
            if (p1 < p2) {
                swap(A, p1++, p2--);
            }
        }

        return A;
    }

    private void swap(int[] nums, int p1, int p2) {
        int temp = nums[p1];
        nums[p1] = nums[p2];
        nums[p2] = temp;
    }
}
```
