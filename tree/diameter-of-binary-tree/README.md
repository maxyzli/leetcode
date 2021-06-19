# Diameter of Binary Tree

## Solution 1

DFS

```java
/**
 * Question   : Diameter of Binary Tree
 * Complexity : Time: O(n) ; Space: O(h)
 * Topics     : Tree
 */
class Solution {
    int maxDiameter = 0;

    public int diameterOfBinaryTree(TreeNode root) {
        maxDiameter = 0;
        findDiameter(root);
        return maxDiameter;
    }

    private int findDiameter(TreeNode tree) {
        if (tree == null) {
            return 0;
        }

        int leftDiameter = findDiameter(tree.left);
        int rightDiameter = findDiameter(tree.right);

        int diameter = leftDiameter + rightDiameter;
        maxDiameter = Math.max(maxDiameter, diameter);

        return 1 + Math.max(leftDiameter, rightDiameter);
    }
}
```
