# Find All Duplicates in an Array

## Solution 1

```java
/**
 * Question   : 442. Find All Duplicates in an Array
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Array
 */
public class Solution {
    public List<Integer> findDuplicates(int[] nums) {
        if (nums == null || nums.length == 0) {
            return new ArrayList<>();
        }

        int increment = nums.length + 1;

        for (int i = 0; i < nums.length; i++) {
            int originNum = nums[i] % increment;
            int index = originNum - 1;
            nums[index] += increment;
        }

        List<Integer> list = new ArrayList<>();

        for (int i = 0; i < nums.length; i++) {
            int count = (nums[i] / increment);
            if (count == 2) {
                list.add(i + 1);
            }
        }

        return list;
    }
}
```

## Solution 2

Mark negative

```java
/**
 * Question   : 442. Find All Duplicates in an Array
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Array
 */
public class Solution {
    public List<Integer> findDuplicates(int[] nums) {
        if (nums == null || nums.length == 0) {
            return new ArrayList<>();
        }

        int increment = nums.length + 1;

        List<Integer> list = new ArrayList<>();

        for (int i = 0; i < nums.length; i++) {
            int index = Math.abs(nums[i]) - 1;
            if (nums[index] < 0) {
                list.add(index + 1);
            } else {
                nums[index] = -nums[index];
            }
        }

        return list;
    }
}
```