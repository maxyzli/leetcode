# Binary Tree Level Order Traversal

## Solution 1

Queue

```java
/**
 * Question   : Binary Tree Level Order Traversal
 * Complexity : Time: worse O(n) ; Space: O(n)
 */
public class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();

        if (root == null) {
            return result;
        }

        Queue<TreeNode> queue = new LinkedList<>();

        queue.add(root);

        while (!queue.isEmpty()) {
            int nodeCount = queue.size();
            List<Integer> nums = new ArrayList<>();

            for (int count = 0; count < nodeCount; count++) {
                TreeNode temp = queue.remove();
                nums.add(temp.val);
                if (temp.left != null) {
                    queue.add(temp.left);
                }
                if (temp.right != null) {
                    queue.add(temp.right);
                }
            }

            result.add(nums);
        }

        return result;
    }
}
```
