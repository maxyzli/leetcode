# Subsets

## Solution 1

Add the list to result every time.

```java
/**
 * Question   : 78. Subsets
 * Complexity : Time: O(n!) ; Space: O(n)
 * Topics     : Backtracking
 */
public class Solution {
    public List<List<Integer>> subsets(int[] array) {
        if (array == null || array.length == 0) {
            return new LinkedList<>();
        }

        List<Integer> list = new LinkedList<>();
        List<List<Integer>> res = new LinkedList<>();
        int beginIndex = 0;

        getSubsets(array, beginIndex, list, res);

        return res;
    }

    private void getSubsets(int[] array, int beginIndex, List<Integer> list, List<List<Integer>> res) {
        // Add current list to the result every time.
        res.add(new LinkedList<>(list));

        for (int i = beginIndex; i < array.length; i++) {
            list.add(array[i]);
            getSubsets(array, i + 1, list, res);
            // Backtracking
            list.remove(list.size() - 1);
        }
    }
}
```

## Solution 2

Add the list to result until the end.

```java
/**
 * Question   : 78. Subsets
 * Topics     : Backtracking
 * Complexity : Time: O(2^n) ; Space: O(n)
 */
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        if (nums == null || nums.length == 0) {
            return new ArrayList<>();
        }

        List<List<Integer>> res = new ArrayList<>();
        List<Integer> list = new ArrayList<>();
        int beginIndex = 0;

        subsetsUtil(nums, beginIndex, list, res);

        return res;
    }

    private void subsetsUtil(int[] nums, int beginIndex, List<Integer> list, List<List<Integer>> res) {
        if (beginIndex == nums.length) {
            res.add(new ArrayList<>(list));
            return;
        }

				// Doesn't choose the value.
        subsetsUtil(nums, beginIndex + 1, list, res);

        // Choose the value.
        subsetsUtil(nums, beginIndex + 1, list, res);
        list.remove(list.size() - 1);
    }
}
```
