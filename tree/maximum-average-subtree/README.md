# Maximum Average Subtree

## Solution 1

```java
/**
 * Question   : 93. Restore IP Addresses
 * Complexity : Time: O(n) ; Space: O(H)
 * Topics     : Tree
 */
class Solution {
    private class NodeData {
        double sum;
        double nodeCount;
        public NodeData(double sum, double nodeCount) {
            this.sum = sum;
            this.nodeCount = nodeCount;
        }
    }

    private double max;

    public double maximumAverageSubtree(TreeNode root) {
        if (root == null) {
            return 0;
        }

        max = 0.0;

        dfs(root);

        return max;
    }

    private NodeData dfs(TreeNode root) {
        if (root == null) {
            return new NodeData(0, 0);
        }

        NodeData left = dfs(root.left);
        NodeData right = dfs(root.right);

        double sum = left.sum + right.sum + root.val;
        double nodeCount = left.nodeCount + right.nodeCount + 1;
        NodeData nodeData = new NodeData(sum, nodeCount);

        max = Math.max(max, sum / nodeCount);

        return nodeData;
    }
}
```
