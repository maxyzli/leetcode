# Flatten Binary Tree to Linked List

## Solution 1

List

```java
/**
 * Question   : 114. Flatten Binary Tree to Linked List
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Tree
 */
class Solution {
    List<TreeNode> list;

    public void flatten(TreeNode root) {
        if (root == null) {
            return;
        }
        list = new LinkedList<>();
        preorder(root);

        TreeNode prev = list.get(0);
        list.remove(0);
        while (!list.isEmpty()) {
            prev.right = list.get(0);
            prev = prev.right;
            list.remove(0);
        }
    }

    private void preorder(TreeNode root) {
        if (root == null) {
            return;
        }
        list.add(root);
        preorder(root.left);
        preorder(root.right);
        root.left = null;
        root.right = null;
    }
}
```

## Solution 2

Pure Recursion

```java
/**
 Question   : 114. Flatten Binary Tree to Linked List
 Complexity : Time: O(n) ; Space: O(n)
 Topics     : Tree
 */
class Solution {
    public void flatten(TreeNode root) {
        if (root == null) {
            return;
        }
        if (root.left == null && root.right == null) {
            return;
        }

        flatten(root.left);
        flatten(root.right);

        TreeNode originRight = root.right;

        root.right = root.left;
        root.left = null;

        TreeNode temp = root;
        while (temp.right != null) {
            temp = temp.right;
        }

        temp.right = originRight;
    }
}
```
