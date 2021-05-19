# Longest Consecutive Sequence

## Solution 1

Sorting

```java
/**
 * Question   : 128. Longest Consecutive Sequence
 * Complexity : Time: O(nlog(n)) ; Space: O(1)
 * Topics     : Hash Table
 */
class Solution {
    public int longestConsecutive(int[] nums) {
        if (nums.length == 0) {
            return 0;
        }
        
        Arrays.sort(nums);

        int ans = 1;
        int count = 1;

        for (int i = 1; i < nums.length; i++) {
            if (nums[i] - nums[i - 1] == 1) {
                count++;
            } else if (nums[i] - nums[i - 1] > 1) {
                count = 1;
            }
            ans = Math.max(ans, count);
        }

        return ans;
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
