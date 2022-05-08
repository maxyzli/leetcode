# Number of Connected Components in an Undirected Graph

## Solution 1: DFS

```java
// TC: O(V+E), where V is the number of nodes, E is the number of connections
// SC: O(V+E)
class Solution {
    public int countComponents(int n, int[][] edges) {
        List<Integer>[] graph = new List[n];
        
        for (int i = 0; i < n; i++) {
            graph[i] = new ArrayList<>();
        }
        
        for (int[] e : edges) {
            graph[e[0]].add(e[1]);
            graph[e[1]].add(e[0]);
        }
        
        int count = 0;
        boolean[] visited = new boolean[n];
        for (int v = 0; v < n; v++) {
            if (visited[v]) {
                continue;
            }
            count++;
            dfs(graph, v, visited);
        }
        
        return count;
    }
    
    private void dfs(List<Integer>[] graph, int u, boolean[] visited) {
        if (visited[u]) {
            return;
        }
        visited[u] = true;
        for (int v : graph[u]) {
            dfs(graph, v, visited);
        }
    }
}
```
