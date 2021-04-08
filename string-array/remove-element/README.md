# Remove Element

## Solution 1

Two Pointers

```java
/**
 * Question   : 27. Remove Element
 * Topics     : array
 * Complexity : Time: O(n) ; Space: O(1)
 */
class Solution {
    public int removeElement(int[] nums, int val) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int slow = 0, fast = 0;

        while (fast < nums.length) {
            if (nums[fast] != val) {
                nums[slow++] = nums[fast++];
            } else {
                fast++;
            }
        }

        return slow;
    }
}
```
