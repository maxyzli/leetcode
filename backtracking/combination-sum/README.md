# Combination Sum

## Solution 1

```java
/**
 * Question   : 39. Combination Sum
 * Complexity : Time: O(n!) ; Space: O(target)
 * Topics     : Backtracking
 */
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        if (candidates == null || candidates.length == 0) {
            return new LinkedList<>();
        }

        List<Integer> list = new LinkedList<>();
        List<List<Integer>> res = new LinkedList<>();
        int startIdx = 0;

        dfs(candidates, startIdx, target, list, res);

        return res;
    }

    public void dfs(int[] candidates, int startIdx, int target, List<Integer> list, List<List<Integer>> res) {
        if (target == 0) {
            res.add(new LinkedList<>(list));
            return;
        }

        for (int i = startIdx; i < candidates.length; i++) {
            if (target >= candidates[i]) {
                list.add(candidates[i]);
                dfs(candidates, i, target - candidates[i], list, res);
                list.remove(list.size() - 1);
            }
        }
    }
}
```
