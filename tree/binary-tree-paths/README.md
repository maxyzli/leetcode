# Binary Tree Paths

## Solution 1

DFS

```java
/**
 * Question   : 257. Binary Tree Paths
 * Topics     : Tree
 * Complexity : Time: O(n) ; Space: O(log(n))
 */
class Solution {
    StringBuilder sb;
    List<String> list;

    public List<String> binaryTreePaths(TreeNode root) {
        sb = new StringBuilder();
        list = new LinkedList<>();
        binaryTreePathsUtil(root);
        return list;
    }

    private void binaryTreePathsUtil(TreeNode root) {
        if (root == null) {
            return;
        }

        int length = sb.length();

        if (root.left == null && root.right == null) {
            sb.append(root.val);
            list.add(sb.toString());
        } else {
            sb.append(root.val + "->");
        }

        binaryTreePathsUtil(root.left);
        binaryTreePathsUtil(root.right);
        sb.setLength(length);
    }
}
```
