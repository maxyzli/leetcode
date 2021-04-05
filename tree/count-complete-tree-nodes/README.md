# Count Complete Tree Nodes

## Solution 1

Native

```java
/**
 * Question   : 222. Count Complete Tree Nodes
 * Topics     : Tree
 * Complexity : Time: O(n) ; Space: O(log(n))
 */
class Solution {
    public int countNodes(TreeNode root) {
        if (root == null) {
            return 0;
        }
        return 1 + countNodes(root.left) + countNodes(root.right);
    }
}
```

## Solution 2

```java
/**
 * Question   : 222. Count Complete Tree Nodes
 * Topics     : Tree
 * Complexity : Time: O(log n * log n) ; Space: O(log(n))
 */
class Solution {
    public int countNodes(TreeNode root) {
        if (root == null) {
            return 0;
        }

        int leftHeight = 1;
        TreeNode temp = root;
        while (temp.left != null) {
            leftHeight++;
            temp = temp.left;
        }

        int rightHeight = 1;
        temp = root;
        while (temp.right != null) {
            rightHeight++;
            temp = temp.right;
        }

        // Perfect binary tree
        if (leftHeight == rightHeight) {
            return (int)(Math.pow(2, leftHeight)) - 1;
        }

        return 1 + countNodes(root.left) + countNodes(root.right);
    }
}
```
