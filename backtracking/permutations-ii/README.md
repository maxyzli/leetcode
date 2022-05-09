# Permutations II

## Solution 1

With used[] array and make sure we access the same values in order.

```java
/**
 * Question   : 47. Permutations II
 * Complexity : Time: O(n!) ; Space: O(n)
 * Topics     : Backtracking
 */
class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        if (nums == null || nums.length == 0) {
            return new LinkedList<>();
        }

        List<Integer> list = new LinkedList<>();
        List<List<Integer>> res = new LinkedList<>();
        boolean[] used = new boolean[nums.length];

        dfs(nums, used, list, res);

        return res;
    }

    private void dfs(int[] nums, boolean[] used, List<Integer> list, List<List<Integer>> res) {
        if (list.size() == nums.length) {
           res.add(new LinkedList(list));
           return;
        }

        for (int i = 0; i < nums.length; i++) {
						// make sure we access the same values in order.
            if (used[i] || (i != 0 && nums[i - 1] == nums[i] && used[i - 1] == false)) {
                continue;
            }

            list.add(nums[i]);
            used[i] = true;

            dfs(nums, used, list, res);

            list.remove(list.size() - 1);
            used[i] = false;
        }
    }
}
```
