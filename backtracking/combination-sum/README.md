# Combination Sum

## Solution 1

```java
/**
 * Question   : 39. Combination Sum
 * Complexity : Time: O(n!) ; Space: O(n)
 * Topics     : Backtracking
 */
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        if (candidates == null || candidates.length == 0) {
            return new ArrayList<>();
        }
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> list = new ArrayList<>();
        int beginIndex = 0;
        Arrays.sort(candidates);
        combinationSumUtil(candidates, target, beginIndex, list, res);
        return res;
    }

    private void combinationSumUtil(int[] candidates, int target, int beginIndex, List<Integer> list, List<List<Integer>> res) {
        if (target < 0) {
            return;
        }
        if (target == 0) {
            res.add(new ArrayList<>(list));
            return;
        }
        for (int i = beginIndex; i < candidates.length; i++) {
            list.add(candidates[i]);
            combinationSumUtil(candidates, target - candidates[i], i, list, res); // not i + 1 because we can reuse same elements
            list.remove(list.size() - 1);
        }
    }
}
```
