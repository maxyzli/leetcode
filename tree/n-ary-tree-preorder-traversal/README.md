# N-ary Tree Preorder Traversal

## Solution 1

```java
/**
 * Question   : 589. N-ary Tree Preorder Traversal
 * Topics     : Tree
 * Complexity : Time: O(n) ; Space: O(n)
 */
class Solution {
    public List<Integer> preorder(Node root) {
        List<Integer> res = new LinkedList<>();
        dfs(root, res);
        return res;
    }

    private void dfs (Node root, List<Integer> res) {
        if (root == null) {
            return;
        }

        res.add(root.val);

        for (Node node : root.children) {
            dfs(node, res);
        }
    }
}
```
