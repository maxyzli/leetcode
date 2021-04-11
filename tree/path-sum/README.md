# Path Sum

## Solution 1

```java
/**
 * Question   : Path Sum
 * Complexity : Time: O(n) ; Space: O(h)
 * Topics     : Tree
 */
public class Solution {
    public boolean hasPathSum(TreeNode root, int sum) {
        if (root == null) return false;

        int remain = sum - root.val;

        if (root.left == null && root.right == null) {
            return remain == 0;
        }

        return hasPathSum(root.left, remain) || hasPathSum(root.right, remain);
    }
}
```
