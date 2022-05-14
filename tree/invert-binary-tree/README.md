# Invert Binary Tree

## Solution 1: Recursive

```java
// TC: O(n)
// SC: O(h), where h is the hight of the tree.
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null) {
            return null;
        }

        TreeNode left = root.left;
        TreeNode right = root.right;

        root.left = invertTree(right);
        root.right = invertTree(left);

        return root;
    }
}
```

## Solution 2: Iterative

```java
// TC: O(n)
// SC: O(n)
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null) {
            return null;
        }

        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);

        while (!q.isEmpty()) {
            TreeNode node = q.poll();
            TreeNode left = node.left;
            TreeNode right = node.right;

            node.left = right;
            node.right = left;

            if (node.left != null) {
                q.offer(node.left);
            }
            if (node.right != null) {
                q.offer(node.right);
            }
        }

        return root;
    }
}
```
