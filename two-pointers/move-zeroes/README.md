# Move Zeroes

## Solution 1

Two Pointers

```java
/**
 * Question   : Move Zeroes
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : array
 */
class Solution {
    public void moveZeroes(int[] nums) {
        if (nums == null || nums.length == 0) {
            return;
        }

        int slow = 0, fast = 0;

        while (fast < nums.length) {
            if (nums[fast] != 0) {
                swap(nums, slow++, fast++);
            } else {
                fast++;
            }
        }
    }

    private void swap(int[] nums, int slow, int fast) {
        int temp = nums[slow];
        nums[slow] = nums[fast];
        nums[fast] = temp;
    }
}
```
