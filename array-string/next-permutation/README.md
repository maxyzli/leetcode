# Next Permutation

## Solution 1

```java
import java.util.*;

/**
 * Question   : 31. Next Permutation
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public void nextPermutation(int[] nums) {
        if (nums == null || nums.length == 0) {
            return;
        }

        int n = nums.length;

        // example:
        // 12385764
        //        i

        int i = n - 2;
        while (i >= 0) {
            if (nums[i] >= nums[i + 1]) {
                i--;
            } else {
                break;
            }
        }

        // No next permutation.
        if (i == -1) {
            reverse(nums, 0, n - 1);
            return;
        }

        // example:
        // 12385764
        //     i

        // Find the number which is greater than curr number at index i.
        int j = n - 1;
        while (j > i) {
            if (nums[j] > nums[i]) {
                break;
            }
            j--;
        }

        // example:
        // 12385764
        //     i j

        // swap numbers at i and j
        swap(nums, i, j);

        // example:
        // 12386754
        //     i j

        // reverse number from i + 1 to the end.
        reverse(nums, i + 1, n - 1);

        // example:
        // 12386457
        //     i
    }

    private void reverse(int[] nums, int left, int right) {
        while (left < right) {
            swap(nums, left++, right--);
        }
    }

    private void swap(int[] nums, int a, int b) {
        int temp = nums[a];
        nums[a] = nums[b];
        nums[b] = temp;
    }
}
```