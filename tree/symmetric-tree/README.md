# Symmetric Tree

## Solution 1

```java
/**
 * Question   : 110. Balanced Binary Tree
 * Complexity : Time: O(n) ; Space: O(log(n))
 * Topics     : Tree
 * Date       : 2021/04/01
 */
class Solution {
    public boolean isSymmetric(TreeNode root) {
        return isSymmetricUtil(root.left, root.right);
    }

    private boolean isSymmetricUtil(TreeNode left, TreeNode right) {
        if (left == null && right == null) {
            return true;
        }
        if (left == null || right == null) {
            return false;
        }
        if (left.val != right.val) {
            return false;
        }
        return isSymmetricUtil(left.left, right.right) && isSymmetricUtil(left.right, right.left);
    }
}
```
