# Symmetric Tree

## Solution 1

```java
/**
 * Question   : 110. Balanced Binary Tree
 * Complexity : Time: O(n) ; Space: O(log(n))
 * Topics     : Tree
 */
class Solution {
    public boolean isSymmetric(TreeNode root) {
        if (root == null) {
            return true;
        }
        return isSymmetricUtil(root.left, root.right);
    }

    public boolean isSymmetricUtil(TreeNode root1, TreeNode root2) {
        if (root1 == null && root2 == null) {
            return true;
        }
        if (root1 == null || root2 == null) {
            return false;
        }
        if (root1.val != root2.val) {
            return false;
        }
        return isSymmetricUtil(root1.left, root2.right) && isSymmetricUtil(root1.right, root2.left);
    }
}
```
