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

## Solution 2

Two Pointers

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int left = 0;
        int right = nums.length - 1;

        while (left <= right) {
            while (left <= right && nums[left] != val) {
                left++;
            }
            while (left <= right && nums[right] == val) {
                right--;
            }
            if (left <= right) {
                swap(nums, left++, right--);
            }
        }

        return right + 1;
    }

    private void swap(int[] nums, int a, int b) {
        int temp = nums[a];
        nums[a] = nums[b];
        nums[b] = temp;
    }
}
```

## Solution 3

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int left = 0;
        int right = nums.length - 1;

        while (left <= right) {
            if (nums[left] == val) {
                nums[left] = nums[right];
                right--;
            } else {
                left++;
            }
        }

        return right + 1;
    }
}
```
