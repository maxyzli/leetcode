# Binary Tree Zigzag Level Order Traversal

## Solution 1

Queue

```java
/**
 * Question   : 103. Binary Tree Zigzag Level Order Traversal
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Tree
 */
class Solution {
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        if (root == null) {
            return new LinkedList<>();
        }

        Deque<TreeNode> queue = new LinkedList<>();

        queue.offer(root);
        List<List<Integer>> list = new LinkedList<>();
        int level = 1;

        while (!queue.isEmpty()) {
            LinkedList<Integer> temp = new LinkedList<>();
            int size = queue.size();

            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();

                if (level % 2 == 1) {
                    temp.addLast(node.val);
                } else {
                    temp.addFirst(node.val);
                }

                if (node.left != null) {
                    queue.add(node.left);
                }
                if (node.right != null) {
                    queue.add(node.right);
                }
            }

            list.add(temp);
            level++;
        }

        return list;
    }
}
```

## Solution 2

Use array to optimize

```java
/**
 * Question   : 103. Binary Tree Zigzag Level Order Traversal
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Tree
 */
class Solution {
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        if (root == null) {
            return new LinkedList<>();
        }

        Deque<TreeNode> queue = new LinkedList<>();

        queue.offer(root);
        List<List<Integer>> list = new LinkedList<>();
        int level = 1;

        while (!queue.isEmpty()) {
            int size = queue.size();
            Integer[] arr = new Integer[size];

            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();

                if (level % 2 == 1) {
                    arr[i] = node.val;
                } else {
                    arr[size - i - 1] = node.val;
                }

                if (node.left != null) {
                    queue.add(node.left);
                }
                if (node.right != null) {
                    queue.add(node.right);
                }
            }

            list.add(Arrays.asList(arr));
            level++;
        }

        return list;
    }
}
```
