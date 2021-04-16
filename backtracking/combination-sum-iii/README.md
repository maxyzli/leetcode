# Combination Sum III

## Solution 1

Backtracking

```java
/**
 * Question   : 216. Combination Sum III
 * Topics     : Backtracking
 * Complexity : Time: O(n!) ; Space: O(n)
 */
class Solution {
    final int MAX_NUM = 9;

    public List<List<Integer>> combinationSum3(int k, int n) {
        if (k <= 0 || n <= 0) {
            return new ArrayList<>();
        }

        List<List<Integer>> res = new ArrayList<>();
        List<Integer> list = new ArrayList<>();
        int beginNum = 1;

        combinationSum3Util(k, n, beginNum, list, res);

        return res;
    }

    private void combinationSum3Util(int k, int n, int beginNum, List<Integer> list, List<List<Integer>> res) {
        if (n < 0 || k < 0) {
            return;
        }
        if (n == 0 && k == 0) {
            res.add(new ArrayList<>(list));
            return;
        }
        for (int num = beginNum; num <= MAX_NUM; num++) {
            list.add(num);
            combinationSum3Util(k - 1, n - num, num + 1, list, res);
            list.remove(list.size() - 1);
        }
    }
}
```
