# Lowest Common Ancestor of a Binary Search Tree

## Solution 1

Stack

```java
/**
 * Question   : 235. Lowest Common Ancestor of a Binary Search Tree
 * Topics     : Tree
 * Complexity : Time: O(log(n)) ; Space: O(log(n))
 */
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        Stack<TreeNode> s1 = new Stack<>();
        Stack<TreeNode> s2 = new Stack<>();

        findNode(root, p, s1);
        findNode(root, q, s2);

        while (s1.size() > s2.size()) {
            s1.pop();
        }
        while (s2.size() > s1.size()) {
            s2.pop();
        }

        while (!s1.isEmpty()) {
            if (s1.peek() == s2.peek()) {
                return s1.peek();
            }
            s1.pop();
            s2.pop();
        }

        return null;
    }

    private void findNode(TreeNode root, TreeNode target, Stack<TreeNode> s) {
        if (root == null) {
            return;
        }
        s.add(root);
        if (root == target) {
            return;
        } else if (root.val > target.val) {
            findNode(root.left, target, s);
        } else {
            findNode(root.right, target, s);
        }
    }
}
```

## Solution 2

Bottom-Up Recursion

```java
/**
 * Question   : 235. Lowest Common Ancestor of a Binary Search Tree
 * Topics     : Tree
 * Complexity : Time: O(log(n)) ; Space: O(log(n))
 */
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null) {
            return null;
        }
        if (root == p || root == q) {
            return root;
        }

        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);

        if (left != null && right != null) {
            return root;
        } else if (left != null) {
            return left;
        } else {
            return right;
        }
    }
}
```

## Solution 3

Top-Down Recursion

```java
/**
 * Question   : 235. Lowest Common Ancestor of a Binary Search Tree
 * Topics     : Tree
 * Complexity : Time: O(log(n)) ; Space: O(log(n))
 */
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null) {
            return null;
        }
        if (root == p || root == q) {
            return root;
        }
        // Make sure p is always smaller than q.
        if (p.val > q.val) {
            return lowestCommonAncestor(root, q, p);
        }

        if (root.val > p.val && root.val < q.val) {
            return root;
        } else if (root.val < p.val && root.val < q.val) {
            return lowestCommonAncestor(root.right, p, q);
        } else {
            return lowestCommonAncestor(root.left, p, q);
        }
    }
}
```
