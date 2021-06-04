# Max Consecutive Ones III

## Solution 1

Sliding Window

```java
/**
 * Question   : 1004. Max Consecutive Ones III
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Sliding Window
 */
class Solution {
    public int longestOnes(int[] nums, int k) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int windowZeroCount = 0;
        int left = 0;
        int right = 0;
        int max = 0;

        while (right < nums.length) {
            int number = nums[right++];

            if (number == 0) {
                windowZeroCount++;
            }

            while (windowZeroCount > k) {
                int numberToRemove = nums[left++];
                if (numberToRemove == 0) {
                    windowZeroCount--;
                }
            }

            max = Math.max(max, right - left);
        }

        return max;
    }
}
```
