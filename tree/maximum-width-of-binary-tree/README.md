# Maximum Width of Binary Tree

## Solution 1

BFS

```java
/**
 * Question   : 662. Maximum Width of Binary Tree
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Tree
 */
class Solution {
    public int widthOfBinaryTree(TreeNode root) {
        if (root == null) {
            return 0;
        }

        Queue<Node> queue = new LinkedList<>();
        queue.offer(new Node(root, 0));
        int maxWidth = 0;

        while (!queue.isEmpty()) {
            int size = queue.size();
            int startSeqNo = 0;
            int endSeqNo = 0;
            for (int i = 0; i < size; i++) {
                Node curr = queue.poll();
                TreeNode node = curr.node;
                int seqNo = curr.seqNo;

                if (i == 0) {
                    startSeqNo = seqNo;
                }
                if (i == size - 1) {
                    endSeqNo = seqNo;
                }

                if (node.left != null) {
                    queue.offer(new Node(node.left, 2 * seqNo + 1));
                }
                if (node.right != null) {
                    queue.offer(new Node(node.right, 2 * seqNo + 2));
                }
            }

            maxWidth = Math.max(maxWidth, endSeqNo - startSeqNo + 1);
        }

        return maxWidth;
    }
}
```
