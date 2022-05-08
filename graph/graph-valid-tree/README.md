# Graph Valid Tree

## Solution 1: Union Find

```java
// TC: O(E)
// SC: O(V)
class Solution {
    public boolean validTree(int n, int[][] edges) {
        int[] parents = new int[n];
        Arrays.fill(parents, -1);
        
        for (int[] e : edges) {
            int p1 = find(parents, e[0]);
            int p2 = find(parents, e[1]);
            
            if (p1 == p2) {
                return false;
            }
            
            parents[p2] = p1;
        }
        
        return edges.length == n - 1;
    }
    
    private int find(int[] parents, int v) {
        if (parents[v] == -1) {
            return v;
        }
        int parent = find(parents, parents[v]);
        parents[v] = parent;
        return parent;
    }
}
```
