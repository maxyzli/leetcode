# Remove Duplicates from Sorted Array II

## Solution 1

```java
/**
 * Question   : Remove Duplicates from Sorted Array II
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Array
 */
public class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int slow = 2, fast = 2;

        int n = nums.length;

        while (fast < n) {
            if (nums[fast] != nums[slow - 2]) {
                nums[slow] = nums[fast];
                slow++;
            }
            fast++;
        }

        return slow;
    }
}
```

## Solution 2

```java
/**
 * Question   : Remove Duplicates from Sorted Array II
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Array
 */
public class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int slow = 0, fast = 1;

        int n = nums.length;
        int count = 1;

        while (fast < n) {
            if (nums[slow] == nums[fast]) {
                count++;
            } else {
                count = 1;
            }

            if (count <= 2) {
                slow++;
                nums[slow] = nums[fast];
            }

            fast++;
        }

        return slow + 1;
    }
}
```