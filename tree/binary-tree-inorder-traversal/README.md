# Binary Tree Inorder Traversal

## Solution 1

Iteration

```java
/**
 * Question   : 94. Binary Tree Inorder Traversal
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Tree
 */
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        if (root == null) {
            return new LinkedList<>();
        }

        List<Integer> list = new LinkedList<>();

        Stack<TreeNode> stack = new Stack();
        TreeNode curr = root;

        while (curr != null || !stack.isEmpty()) {
            if (curr != null) {
                stack.add(curr);
                curr = curr.left;
                continue;
            } 
            
            TreeNode temp = stack.pop();
            list.add(temp.val);
            curr = temp.right;
        }

        return list;
    }
}
```

## Solution 2

Recursion

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> inorder = new LinkedList<>();
        traversal(root, inorder);
        return inorder;
    }

    private void traversal(TreeNode root, List<Integer> inorder) {
        if (root == null) return;
        traversal(root.left, inorder);
        inorder.add(root.val);
        traversal(root.right, inorder);
    }
}
```
