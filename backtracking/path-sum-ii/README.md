# Path Sum II

## Solution 1

```jsx
/**
 * Question   : 113. Path Sum II
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : BT
 */
class Solution {
    public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
        if (root == null) {
            return new ArrayList<>();
        }
        List<Integer> path = new ArrayList<>();
        List<List<Integer>> res = new ArrayList<>();
        pathSumUtil(root, targetSum, path, res);
        return res;
    }

    private void pathSumUtil(TreeNode root, int targetSum, List<Integer> path, List<List<Integer>> res) {
        if (root == null) {
            return;
        }

        path.add(root.val);
        int sum = targetSum - root.val;

        if (sum == 0 && root.left == null && root.right == null) {
            res.add(new ArrayList<>(path));
        }

        pathSumUtil(root.left, sum, path, res);
        pathSumUtil(root.right, sum, path, res);
        path.remove(path.size() - 1);
    }
}
```
