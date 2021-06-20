# Remove Duplicates from Sorted Array

## Solution 1

Two Pointers

```java
class Solution {
    private int MAX_DUP_ALLOW = 1;

    public int removeDuplicates(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int duplicateCount = 0;
        int currNum = nums[0];
        int slow = 0;
        int fast = 0;

        for (; fast < nums.length; fast++) {
            if (nums[fast] == currNum) {
                duplicateCount++;
            } else {
                currNum = nums[fast];
                duplicateCount = 1;
            }
            if (duplicateCount <= MAX_DUP_ALLOW) {
                nums[slow] = nums[fast];
                slow++;
            }
        }

        return slow;
    }
}
```
