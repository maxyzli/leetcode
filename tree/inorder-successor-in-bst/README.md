# Inorder Successor in BST

## Solution 1

```java

/**
 * Question   : 285. Inorder Successor in BST
 * Complexity : Time: O(H) ; Space: O(H)
 * Topics     : BST
 */
class Solution {
    TreeNode candidate = null;

    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        if (root == null) {
            return root;
        }

        if (root.val > p.val) { // go left
            candidate = root;
            return inorderSuccessor(root.left, p);
        } else if (root.val < p.val) { // go right
            return inorderSuccessor(root.right, p);
        } else { // root == p
            if (p.right == null) {
                return candidate;
            } else {
                return findSmallest(root.right);
            }
        }
    }

    private TreeNode findSmallest(TreeNode root) {
        TreeNode curr = root;;
        while (curr.left != null) {
            curr = curr.left;
        }
        return curr;
    }
}
```
