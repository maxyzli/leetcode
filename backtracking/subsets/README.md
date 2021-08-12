# Subsets

## Solution 1

```java
/**
 * Question   : 78. Subsets
 * Complexity : Time: O(2^n) ; Space: O(n)
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
