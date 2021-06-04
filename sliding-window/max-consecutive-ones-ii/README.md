# Max Consecutive Ones II

## Solution 1

```java
/**
 * Question   : 487. Max Consecutive Ones II
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Sliding Window
 */
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
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
            
            while (windowZeroCount > 1) {
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

## Solution 2

```java
/**
 * Question   : 487. Max Consecutive Ones II
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Sliding Window
 */
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int zeroIndex = -1;
        int left = 0;
        int right = 0;
        int max = 0;

        while (right < nums.length) {
            int number = nums[right];

            if (number == 0) {
                if (zeroIndex >= 0) {
                    max = Math.max(max, right - left);
                    left = zeroIndex + 1;
                }
                zeroIndex = right;
            }

            right++;
        }

        return Math.max(max, right - left);
    }
}
```
