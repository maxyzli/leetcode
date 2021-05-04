# Missing Ranges

## Solution 1

```java
/**
 * Question   : 163. Missing Ranges
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public List<String> findMissingRanges(int[] nums, int lower, int upper) {
        List<String> list = new ArrayList<>();

        int pre = lower - 1;

        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == pre + 2) {
                list.add((pre + 1) + "");
            } else if (nums[i] > pre + 2) {
                list.add((pre + 1) + "->" + (nums[i] - 1));
            }
            pre = nums[i];
        }

        if (upper == pre + 1) {
            list.add((pre + 1) + "");
        } else if (upper > pre + 1) {
            list.add((pre + 1) + "->" + upper);
        }

        return list;
    }
}
```