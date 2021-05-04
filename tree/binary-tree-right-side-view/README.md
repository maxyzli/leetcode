# Binary Tree Right Side View

## Solution 1

Queue

# Solution 1

Queue

```java
/**
 * Question   : 199. Binary Tree Right Side View
 * Complexity : Time: O(n) ; Space: O(log(n))
 * Topics     : Tree
 */
class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        if (root == null) {
            return new LinkedList<>();
        }

        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);

        List<Integer> list = new ArrayList<>();

        while (!q.isEmpty()) {
            int size = q.size();
            for (int i = 0; i < size; i++) {
                TreeNode temp = q.remove();
                if (temp.left != null) {
                    q.add(temp.left);
                }
                if (temp.right != null) {
                    q.add(temp.right);
                }
                // Last one in this level.
                if (i == size - 1) {
                    list.add(temp.val);
                }
            }
        }

        return list;
    }
}
```
