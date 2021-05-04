# Find All Numbers Disappeared in an Array

## Solution 1

```java
/**
 * Question   : 448. Find All Numbers Disappeared in an Array
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public List<Integer> findDisappearedNumbers(int[] nums) {
        if (nums == null || nums.length == 0) {
            return new ArrayList<>();
        }

        List<Integer> list = new ArrayList<>();

        int increment = nums.length + 1;

        for (int i = 0; i < nums.length; i++) {
            int originNum = nums[i] % increment;
            int index = originNum - 1;
            nums[index] += increment;
        }

        for (int i = 0; i < nums.length; i++) {
            if (nums[i] / increment == 0) {
                list.add(i + 1);
            }
        }

        return list;
    }
}
```