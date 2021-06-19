# Binary Tree Preorder Traversal

## Solution 1

Iteration

```jsx
/**
 * Question   : 144. Binary Tree Preorder Traversal
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Tree
 */
public class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        if (root == null) {
            return new LinkedList<>();
        }

        List<Integer> list = new LinkedList<>();

        Stack<TreeNode> stack = new Stack<>();
        stack.add(root);
        while (!stack.isEmpty()) {
            TreeNode temp = stack.pop();
            list.add(temp.val);
            if (temp.right != null) {
                stack.add(temp.right);
            }
            if (temp.left != null) {
                stack.add(temp.left);
            }
        }

        return list;
    }
}
```

## Solution 2

Recustion

```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> res = new LinkedList<>();
        traversal(root, res);
        return res;
    }

    private void traversal(TreeNode root, List<Integer> res) {
        if (root == null) return;
        res.add(root.val);
        traversal(root.left, res);
        traversal(root.right, res);
    }
}
```
