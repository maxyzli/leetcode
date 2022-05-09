# Sort Array By Parity II

## Solution 1

Temporary dpry

```java
/**
 * Question   : 922. Sort Array By Parity II
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Array
 */
class Solution {
    public int[] sortArrayByParityII(int[] nums) {
        if (nums == null || nums.length == 0) {
            return nums;
        }

        int[] temp = new int[nums.length];

        int evenIdx = 0;
        int oddIdx = 1;

        for (int i = 0; i < nums.length; i++) {
            if (nums[i] % 2 == 0) {
                temp[evenIdx] = nums[i];
                evenIdx += 2;
            } else {
                temp[oddIdx] = nums[i];
                oddIdx += 2;
            }
        }

        return temp;
    }
}
```

## Solution 2

Two Pointers

```java
/**
 * Question   : 922. Sort Array By Parity II
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public int[] sortArrayByParityII(int[] nums) {
        if (nums == null || nums.length == 0) {
            return nums;
        }

        int n = nums.length;
        int even = 0;
        int odd = 1;

        while (even < n && odd < n) {
            while (even < n && nums[even] % 2 == 0) {
                even += 2;
            }
            while (odd < n && nums[odd] % 2 == 1) {
                odd += 2;
            }
            if (even < n && odd < n) {
                swap(nums, even, odd);
            }
        }

        return nums;
    }

    private void swap(int[] nums, int even, int odd) {
        int temp = nums[even];
        nums[even] = nums[odd];
        nums[odd] = temp;
    }
}
```
