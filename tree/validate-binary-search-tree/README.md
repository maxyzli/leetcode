# Validate Binary Search Tree

## Solution 1

```java
class Solution {
    Integer currMax;

    public boolean isValidBST(TreeNode root) {
        return traverse(root);
    }

    public boolean traverse(TreeNode root) {
        if (root == null) {
            return true;
        }

        if (!traverse(root.left)) {
            return false;
        }

        if (currMax != null) {
            if (currMax.compareTo(root.val) >= 0) {
                return false;
            }
        }
        currMax = root.val;

        if (!traverse(root.right)) {
            return false;
        }

        return true;
    }
}
```

## Solution 2

```java
/**
 * Question   : Validate Binary Search Tree
 * Complexity : Time: O(n) ; Space: O(h)
 * Topics     : BST
 */
class Solution {
    public boolean isValidBST(TreeNode root) {
        return isValidBST(root, null, null);
    }

    private boolean isValidBST(TreeNode root, TreeNode upperBound, TreeNode lowerBound) {
        if (root == null) {
            return true;
        }

        if (upperBound != null && root.val >= upperBound.val) return false;
        if (lowerBound != null && root.val <= lowerBound.val) return false;

        return isValidBST(root.left, root, lowerBound) && isValidBST(root.right, upperBound, root);
    }
}
```
