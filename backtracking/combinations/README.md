# Combinations

## Solution 1

```java
/**
 * Question   : 77. Combinations
 * Complexity : Time: O(n!) ; Space: O(n)
 * Topics     : Backtracking
 */
class Solution {
    public List<List<Integer>> combine(int n, int k) {
        if (n <= 0 || k <= 0 || k > n) {
            return new ArrayList<>();
        }
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> list = new ArrayList<>();
        int begin = 1;
        combineUtil(n, k, begin, list, res);
        return res;
    }

    private void combineUtil(int n, int k, int begin, List<Integer> list, List<List<Integer>> res) {
        if (list.size() == k) {
            res.add(new ArrayList<>(list));
            return;
        }
        for (int num = begin; num <= n; num++) {
            list.add(num);
            combineUtil(n, k, num + 1, list, res);
            list.remove(list.size() - 1);
        }
    }
}
```
