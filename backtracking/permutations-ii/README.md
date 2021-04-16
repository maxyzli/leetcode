# Permutations II

## Solution 1

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

        Arrays.sort(nums);

        List<List<Integer>> res = new LinkedList<>();
        List<Integer> list = new LinkedList<>();
        // Store used numbers.
        boolean[] used = new boolean[nums.length];

        getPermutation(nums, list, res, used);

        return res;
    }

    private void getPermutation(int[] nums, List<Integer> list, List<List<Integer>> res, boolean[] used) {
        if (list.size() == nums.length) {
            res.add(new LinkedList<>(list));
            return;
        }

        for (int i = 0; i < nums.length; i++) {
            // Remove duplicated.
            if (used[i]) {
                continue;
            }

            //                      (0)
            //                       |
            //       [1(a)          1(b)            2]
            //         |             |              |
            //   [1(a) 1(b) 2] [1(a) 1(b) 2] [1(a) 1(b) 2]
            //   ...

            // nums[i] == nums[i - 1] && !used[i - 1]:
            // This means current value is the same as previous number and we traverse previous number before.
            if (i > 0 && nums[i] == nums[i - 1] && !used[i - 1]) {
                continue;
            }

            list.add(nums[i]);
            used[i] = true;

            getPermutation(nums, list, res, used);

            // Backtracking
            list.remove(list.size() - 1);
            used[i] = false;
        }
    }
}
```
