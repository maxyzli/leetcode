# Remove Duplicates from Sorted Array

## Solution 1

Two Pointers

```java
/**
 * Question   : 26. Remove Duplicates from Sorted Array
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : string
 */
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int slow = 0;
        int fast = 0;

        int n = nums.length;

        while (fast < n) {
            int num = nums[slow];
            while (fast < n && nums[fast] == num) {
                fast++;
            }
            if (fast < n) {
                nums[++slow] = nums[fast];
            }
        }

        return slow + 1;
    }
}
```
