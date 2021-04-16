# Subsets II

## Solution 1

```java
/**
 * Question   : 90. Subsets II
 * Complexity : Time: O(n!) ; Space: O(n)
 * Topics     : Backtracking
 */
public class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        if (nums == null || nums.length == 0) {
            return new ArrayList<>();
        }

        Arrays.sort(nums);

        List<List<Integer>> res = new ArrayList<>();
        List<Integer> list = new ArrayList<>();
        int beginIndex = 0;

        subsetsWithDupUtil(nums, beginIndex, list, res);

        return res;
    }

    private void subsetsWithDupUtil(int[] nums, int beginIndex, List<Integer> list, List<List<Integer>> res) {
        res.add(new ArrayList<>(list));

        for (int i = beginIndex; i < nums.length; i++) {
            // Remove duplicates.
            if (i > beginIndex && nums[i - 1] == nums[i]) {
                continue;
            }
            list.add(nums[i]);
            subsetsWithDupUtil(nums, i + 1, list, res);
            list.remove(list.size() - 1);
        }
    }
}
```
