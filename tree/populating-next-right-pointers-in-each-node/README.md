# Populating Next Right Pointers in Each Node

## Solution 1

Queue

```java
/**
 * Question   : 116. Populating Next Right Pointers in Each Node
 * Topics     : Tree
 * Complexity : Time: O(n) ; Space: O(n)
 */
class Solution {
    public Node connect(Node root) {
        if (root == null) {
            return null;
        }

        Queue<Node> q = new LinkedList<>();
        q.add(root);

        while (!q.isEmpty()) {
            int size = q.size();
            Node prev = null;
            for (int i = 0; i < size; i++) {
                Node temp = q.remove();
                if (temp.left != null) {
                    q.add(temp.left);
                }
                if (temp.right != null) {
                    q.add(temp.right);
                }
                // Handle next pointer.
                if (prev != null) {
                    prev.next = temp;
                }
                prev = temp;
            }
        }

        return root;
    }
}
```

## Solution 2

Recursion

```java
/**
 * Question   : 116. Populating Next Right Pointers in Each Node
 * Topics     : Tree
 * Complexity : Time: O(n) ; Space: O(log(n))
 */
class Solution {
    public Node connect(Node root) {
        if (root == null) {
            return null;
        }
        // No child to connect.
        if (root.left == null) {
            return root;
        }

        // Handle child connection.
        root.left.next = root.right;

        // Handle child connection across border.
        if (root.next != null && root.right != null) {
            root.right.next = root.next.left;
        }

        connect(root.left);
        connect(root.right);

        return root;
    }
}
```
