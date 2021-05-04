# Maximum Gap

## Solution 1

Sorting

```java
/**
 * Question   : 164. Maximum Gap
 * Complexity : Time: O(nlog(n)) ; Space: O(n)
 * Topics     : array
 */
class Solution {
    public int maximumGap(int[] nums) {
        if (nums == null || nums.length <= 1) {
            return 0;
        }

        Arrays.sort(nums);

        int maxGap = 0;
        for (int i = 0; i < nums.length - 1; i++) {
            maxGap = Math.max(maxGap, nums[i + 1] - nums[i]);
        }

        return maxGap;
    }
}
```

## Solution 2

Radix Sort

```java
import java.util.*;

/**
 * Question   : 164. Maximum Gap
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : array
 */
class Solution {
    public int maximumGap(int[] nums) {
        if (nums == null || nums.length <= 1) {
            return 0;
        }

        radixSort(nums);

        int maxGap = 0;
        for (int i = 0; i < nums.length - 1; i++) {
            maxGap = Math.max(maxGap, nums[i + 1] - nums[i]);
        }

        return maxGap;
    }

    private void radixSort(int[] nums) {
        // 1. Find max value.
        int maxVal = nums[0];
        for (int i = 1; i < nums.length; i++) {
            maxVal = Math.max(maxVal, nums[i]);
        }

        // Sort by digit.
        for (int exp = 1; maxVal / exp > 0; exp *= 10) {
            radixSortUtil(nums, exp);
        }
    }

    private void radixSortUtil(int[] nums, int exp) {
        // 0 - 9
        int[] counts = new int[10];

        // Count digits
        for (int i = 0; i < nums.length; i++) {
            int digit = (nums[i] / exp) % 10;
            counts[digit]++;
        }

        // Accumulation
        for (int i = 1; i < counts.length; i++) {
            counts[i] += counts[i - 1];
        }

        int[] output = new int[nums.length];
        for (int i = nums.length - 1; i >= 0; i--) {
            int digit = (nums[i] / exp) % 10;
            int index = counts[digit] - 1;
            output[index] = nums[i];
            counts[digit]--;
        }

        for (int i = 0; i < output.length; i++) {
            nums[i] = output[i];
        }
    }
}
```
