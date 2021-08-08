# N-ary Tree Level Order Traversal

## Solution 1

BFS

```java
/**
 * Question   : 429. N-ary Tree Level Order Traversal
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Tree
 */
class Solution {
    public List<List<Integer>> levelOrder(Node root) {
        if (root == null) {
            return new LinkedList<>();
        }
        
        List<List<Integer>> list = new LinkedList<>();
        
        Queue<Node> queue = new LinkedList<>();
        queue.offer(root);
        
        while (queue.size() != 0) {
            List<Integer> temp = new LinkedList<>();
            int size = queue.size();
            
            for (int i = 0; i < size; i++) {
                Node node = queue.poll();
                temp.add(node.val);
                // Add children to the queue.
                for (Node child : node.children) {
                    queue.add(child);
                }
            }
            
            list.add(temp);
        }
        
        return list;
    }
}
```
