# Summary Ranges

## Solution 1

```java
/**
 * Question   : 228. Summary Ranges
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public List<String> summaryRanges(int[] nums) {
        if (nums == null || nums.length == 0) {
            return new ArrayList<>();
        }

        int n = nums.length;
        int i = 0;
        List<String> list = new ArrayList<>();

        while (i < n) {
            int beginIdx = i;
            i++;

            while (i < n && nums[i] - nums[i - 1] == 1) {
               i++;
            }

            int endIdx = i - 1;

            if (beginIdx != endIdx) {
                list.add(nums[beginIdx] + "->" + nums[endIdx]);
            } else {
                list.add(nums[beginIdx] + "");
            }
        }

        return list;
    }
}
```
