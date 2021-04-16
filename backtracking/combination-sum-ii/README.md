# Combination Sum II

## Solution 1

With `used[]` array

```java
/**
 * Question   : 40. Combination Sum II
 * Complexity : Time: O(n!) ; Space: O(n)
 * Topics     : Backtracking
 */
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        if (candidates == null || candidates.length == 0) {
            return new ArrayList<>();
        }
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> list = new ArrayList<>();
        boolean[] used = new boolean[candidates.length];
        int beginIndex = 0;
        Arrays.sort(candidates);
        combinationSumUtil(candidates, target, beginIndex, used, list, res);
        return res;
    }

    private void combinationSumUtil(int[] candidates, int target, int beginIndex, boolean[] used, List<Integer> list, List<List<Integer>> res) {
        if (target < 0) {
            return;
        }
        if (target == 0) {
            res.add(new ArrayList<>(list));
            return;
        }
        for (int i = beginIndex; i < candidates.length; i++) {
			// candidates[i - 1] == candidates[i - 1] && !used[i - 1]:
            // This means current value is the same as previous number and we traverse previous number before.
            if (i > 0 && (candidates[i - 1] == candidates[i] && used[i - 1] == false)) {
                continue;
            }

            used[i] = true;
            list.add(candidates[i]);

            combinationSumUtil(candidates, target - candidates[i], i + 1, used, list, res);

            used[i] = false;
            list.remove(list.size() - 1);
        }
    }
}
```

## Solution 2

Without `used[]` array

```java
import java.util.*;

/**
 * Question   : 39. Combination Sum
 * Complexity : Time: O(n!) ; Space: O(n)
 * Topics     : Backtracking
 */
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
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
            // We solve the question without using the used[] array here, since i is not start from beginning.
            // It's a little bit different from Permutations II.
            if (i > beginIndex && (candidates[i - 1] == candidates[i])) {
                continue;
            }
            list.add(candidates[i]);
            combinationSumUtil(candidates, target - candidates[i], i + 1, list, res);
            // Backtracking
            list.remove(list.size() - 1);
        }
    }
}
```
