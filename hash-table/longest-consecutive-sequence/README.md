# Longest Consecutive Sequence

## Solution 1: Set

```java
// TC: O(n)
// SC: (n)
class Solution {
    public int longestConsecutive(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        Set<Integer> set = new HashSet<>();

        for (int num : nums) {
            set.add(num);
        }

        int maxCount = 1;
        for (int num : nums) {
            if (!set.contains(num)) {
                continue;
            }

            int left = num - 1;
            int right = num + 1;

            int count = 1;
            while (set.contains(left)) {
                set.remove(left);
                count++;
                left--;
            }
            while (set.contains(right)) {
                set.remove(right);
                count++;
                right++;
            }

            maxCount = Math.max(maxCount, count);
        }


        return maxCount;
    }
}
```

## Solution 2

Hash Map `O(n^2)`

```java
/**
 * Question   : Longest Consecutive Sequence
 * Complexity : Time: O(n^2) ; Space: O(n)
 * Topics     : Array
 */
class Solution {
    public int longestConsecutive(int[] array) {
        Set<Integer> set = new HashSet<>();

        // Store all the number inside a set.
        for (int i = 0; i < array.length; i++) {
            set.add(array[i]);
        }

        int ans = 0;

        for (int i = 0; i < array.length; i++) {
            int num = array[i];
            int len = 1;

            // Find next consecutive number.
            while (set.contains(num + len)) {
                len++;
            }

            ans = Math.max(ans, len);
        }

        return ans;
    }
}
```

## Solution 3

Hash Map `O(n)`

```java
/**
 * Question   : Longest Consecutive Sequence
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Array
 */
class Solution {
    public int longestConsecutive(int[] nums) {
        Set<Integer> set = new HashSet<>();

        // Store all the number inside a set.
        for (int i = 0; i < nums.length; i++) {
            set.add(nums[i]);
        }

        int ans = 0;

        for (int i = 0; i < nums.length; i++) {
            // If previous value exists we should skip current value.
		    // Because when calculating the length for previous value will definitely contains current value.
            if (set.contains(nums[i] - 1)) {
                continue;
            }

            int num = nums[i];
            int len = 1;

            // Find next consecutive number.
            while (set.contains(num + len)) {
                len++;
            }

            ans = Math.max(ans, len);
        }

        return ans;
    }
}
```

## Solution 4

Hash Map `O(n)`

```java
/**
 * Question   : Longest Consecutive Sequence
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Array
 */
class Solution {
    public int longestConsecutive(int[] array) {
        Set<Integer> set = new HashSet<>();

        // Store all the number inside a set.
        for (int i = 0; i < array.length; i++) {
            set.add(array[i]);
        }

        int ans = 0;

        for (int i = 0; i < array.length; i++) {
            int num = array[i];

            int len = 1;
            int left = num - 1;
            int right = num + 1;

            // Expend the smaller consecutive number.
            while (set.contains(left)) {
                set.remove(left);
                len++;
                left--;
            }

            // Expend the bigger consecutive number.
            while (set.contains(right)) {
                set.remove(right);
                len++;
                right++;
            }

            ans = Math.max(ans, len);
        }

        return ans;
    }
}
```
