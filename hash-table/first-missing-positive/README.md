# First Missing Positive

## Solution 1

Brute Force (Time Limit Exceeded)

```java
/**
 * Question   : 41. First Missing Positive
 * Topics     : Hash Table
 * Complexity : Time: O(n^2) ; Space: O(1)
 */
class Solution {
    public int firstMissingPositive(int[] nums) {
        for (int positiveNum = 1; positiveNum <= nums.length; positiveNum++) {
            boolean isExist = false;

            for (int i = 0; i < nums.length; i++) {
                if (nums[i] == positiveNum) {
                    isExist = true;
                }
            }

            if (!isExist) {
                return positiveNum;
            }
        }

        return nums.length + 1;
    }
}
```

## Solution 2

Hash Table

```java
/**
 * Question   : 41. First Missing Positive
 * Topics     : Hash Table
 * Complexity : Time: O(n) ; Space: O(n)
 */
class Solution {
    public int firstMissingPositive(int[] nums) {
        Set<Integer> set = new HashSet<>();

        for (int i = 0; i < nums.length; i++) {
            set.add(nums[i]);
        }

        for (int positiveNum = 1; positiveNum <= nums.length; positiveNum++) {
            if (!set.contains(positiveNum)) {
                return positiveNum;
            }
        }

        return nums.length + 1;
    }
}
```

## Solution 3

```java
/**
 * Question   : 41. First Missing Positive
 * Topics     : Hash Table
 * Complexity : Time: O(n) ; Space: O(1)
 */
class Solution {
    public int firstMissingPositive(int[] nums) {
        int n = nums.length;

        for (int i = 0; i < n; i++) {
            if (nums[i] <= 0) {
                // Replace negative numbers to a value we won't consider.
                nums[i] = n + 1;
            }
        }

        for (int i = 0; i < n; i++) {
            int num = Math.abs(nums[i]);
            if (num <= n) {
                nums[num - 1] = -Math.abs(nums[num - 1]);
            }
        }

        for (int i = 0; i < n; i++) {
            if (nums[i] > 0) {
                return i + 1;
            }
        }

        return n + 1;
    }
}
```
