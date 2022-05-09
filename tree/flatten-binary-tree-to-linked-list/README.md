# Flatten Binary Tree to Linked List

## Solution 1

Preorder

```jsx
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

        TreeNode curr = list.get(0);
        for (int i = 1; i < list.size(); i++) {
            TreeNode next = list.get(i);
            curr.right = next;
            curr = next;
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

Recursion

```java
/**
 Question   : 114. Flatten Binary Tree to Linked List
 Complexity : Time: O(n) ; Space: O(log(h))
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

        TreeNode curr = root;
        while (curr.right != null) {
            curr = curr.right;
        }
        curr.right = originRight;
    }
}
```
