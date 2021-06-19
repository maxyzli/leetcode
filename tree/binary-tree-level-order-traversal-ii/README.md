# Binary Tree Level Order Traversal II

## Solution 1

key: `list.addFirst`

```java
/**
 * Question   : 107. Binary Tree Level Order Traversal II
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Tree
 */
public class Solution {
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        if (root == null) {
            return new LinkedList<>();
        }

        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);

        LinkedList<List<Integer>> res = new LinkedList<>();

        while (!q.isEmpty()) {
            int size = q.size();
            List<Integer> currLevel = new LinkedList<>();
            for (int i = 0; i < size; i++) {
                TreeNode node = q.remove();
                currLevel.add(node.val);
                if (node.left != null) {
                    q.add(node.left);
                }
                if (node.right != null) {
                    q.add(node.right);
                }
            }
            res.addFirst(currLevel);
        }

        return res;
    }
}
```
