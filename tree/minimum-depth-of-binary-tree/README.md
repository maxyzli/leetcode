# Minimum Depth of Binary Tree

## Solution 1

DFS

```java
class Solution {
    public int minDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }

        int leftDepth = minDepth(root.left);
        int rightDepth = minDepth(root.right);

        if (leftDepth != 0 && rightDepth != 0) {
            return 1 + Math.min(leftDepth, rightDepth);
        } else if (leftDepth == 0) {
            return 1 + rightDepth;
        } else {
            return 1 + leftDepth;
        }
    }
}
```

## Solution 2

BFS

```java
class Solution {
    public int minDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }

        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);

        int level = 0;
        while (!q.isEmpty()) {
            level++;
            int size = q.size();

            for (int i = 0; i < size; i++) {
                TreeNode temp = q.remove();
                if (temp.left == null && temp.right == null) {
                    return level;
                }
                if (temp.left != null) {
                    q.add(temp.left);
                }
                if (temp.right != null) {
                    q.add(temp.right);
                }
            }
        }

        return 0;
    }
}
```
