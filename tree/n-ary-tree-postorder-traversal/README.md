# N-ary Tree Postorder Traversal

## Solution 1

```java
/**
 * Question   : 590. N-ary Tree Postorder Traversal
 * Topics     : Tree
 * Complexity : Time: O(n) ; Space: O(n)
 */
class Solution {
    public List<Integer> postorder(Node root) {
        if (root == null) {
            return new LinkedList<>();
        }
        List<Integer> res = new LinkedList<>();
        dfs(root, res);
        return res;
    }
    
    private void dfs(Node root, List<Integer> res) {
        if (root == null) {
            return;
        }
        
        for (Node node : root.children) {
            dfs(node, res);
        }
        
        res.add(root.val);
    }
}
```
