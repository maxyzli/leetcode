# Binary Search Tree Iterator

## Solution 1

```java
/**
 Question   : 173. Binary Search Tree Iterator
 Complexity : Time: O(n) ; Space: O(n)
 Topics     : Tree
 */
class BSTIterator {
    TreeNode curr;
    Stack<TreeNode> stack;

    public BSTIterator(TreeNode root) {
        this.stack = new Stack<>();
        this.curr = root;
    }

    public int next() {
        if (curr != null || !stack.isEmpty()) {
            while (curr != null) {
                stack.add(curr);
                curr = curr.left;
            }
            TreeNode popped = stack.pop();
            curr = popped.right;
            return popped.val;
        }
        return Integer.MIN_VALUE;
    }

    public boolean hasNext() {
        return curr != null || !stack.isEmpty();
    }
}
```
