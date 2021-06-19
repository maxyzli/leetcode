# Sum of Left Leaves

## Solution 1

BFS

```java
class Solution {
    public int sumOfLeftLeaves(TreeNode root) {
        Queue<TreeNode> queue = new ArrayDeque<>();

        int sum = 0;
        queue.offer(root);

        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                if (node.left != null) {
                    if (node.left.left == null && node.left.right == null) {
                        sum += node.left.val;
                    }
                    queue.offer(node.left);
                }
                if (node.right != null) {
                    queue.offer(node.right);
                }
            }
        }

        return sum;
    }
}
```

## Solution 2

DFS

```java
class Solution {
    int sum = 0;

    public int sumOfLeftLeaves(TreeNode root) {
        sum = 0;
        dfs(root, root);
        return sum;
    }

    private void dfs(TreeNode node, TreeNode parent) {
        if (node == null) {
            return;
        }

        if (node.left == null && node.right == null && node == parent.left) {
            sum += node.val;
        }

        dfs(node.left, node);
        dfs(node.right, node);
    }
}
```
