# Path Sum III

## Solution 1

```java
/**
 * Question   : 113. Path Sum II
 * Complexity : Time: O(n^2) ; Space: O(log(n))
 * Topics     : BT
 */
class Solution {
    int count;

    public int pathSum(TreeNode root, int targetSum) {
        if (root == null) {
            return 0;
        }
        count = 0;
        traverse(root, targetSum);
        return count;
    }

    private void traverse(TreeNode root, int targetSum) {
        if (root == null) {
            return;
        }
        pathSumUtil(root, targetSum);
        traverse(root.left, targetSum);
        traverse(root.right, targetSum);
    }

    private void pathSumUtil(TreeNode root, int targetSum) {
        if (root == null) {
            return;
        }

        int sum = targetSum - root.val;
        if (sum == 0) {
            count++;
        }

        pathSumUtil(root.left, sum);
        pathSumUtil(root.right, sum);
    }
}
```
