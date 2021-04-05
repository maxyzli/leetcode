# Summary Ranges

## Solution 1

```java
/**
 * Question   : 228. Summary Ranges
 * Topics     : String
 * Complexity : Time: O(n) ; Space: O(n)
 */
class Solution {
    public List<String> summaryRanges(int[] nums) {
        if (nums == null || nums.length == 0) {
            return new LinkedList<>();
        }

        int n = nums.length;

        int first = nums[0];
        int len = 1;

        List<String> list = new LinkedList<>();

        for (int i = 1; i < n; i++) {
            if (nums[i] == first + len) {
                len++;
                continue;
            }

            if (len == 1) {
                list.add(first + "");
            } else {
                list.add(first + "->" + nums[i - 1]);
            }

            first = nums[i];
            len = 1;
        }

        if (len == 1) {
            list.add(first + "");
        } else {
            list.add(first + "->" + nums[n - 1]);
        }

        return list;
    }
}
```
