# Lowest Common Ancestor of a Binary Search Tree

## Solution 1

Native Solution

```java
/**
 * Question   : 235. Lowest Common Ancestor of a Binary Search Tree
 * Topics     : Tree
 * Complexity : Time: O(n) ; Space: O(log(n))
 */
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null) {
            return null;
        }
        if (root == p || root == q) {
            return root;
        }

        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);

        if (left != null && right != null) {
            return root;
        } else if (left != null) {
            return left;
        } else {
            return right;
        }
    }
}
```

## Solution 2

Leverage Binary Search Tree

```java
/**
 * Question   : 235. Lowest Common Ancestor of a Binary Search Tree
 * Topics     : Tree
 * Complexity : Time: O(log(n)) ; Space: O(log(n))
 */
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root.val > p.val && root.val > q.val) {
            return lowestCommonAncestor(root.left, p, q);
        } else if (root.val < p.val && root.val < q.val) {
            return lowestCommonAncestor(root.right, p, q);
        } else {
            // other cases
            // 1. root == p || root == q
            // 2. root > p.val && root < q.val
            // 3. root < p.val && root > q.val
            return root;
        }
    }
}
```
