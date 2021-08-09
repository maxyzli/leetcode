# Employee Importance

## Solution 1

```java
/**
 * Question   : 690. Employee Importance
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Tree
 */
class Solution {
    Map<Integer, Employee> idToEmployee;
    
    public int getImportance(List<Employee> employees, int id) {
        idToEmployee = new HashMap<>();
        
        for (Employee e : employees) {
            idToEmployee.put(e.id, e);
        }
        
        return dfs(id);
    }
    
    private int dfs(int id) {
        Employee e = idToEmployee.get(id);
        
        int importance = e.importance;
        
        for (int subID : e.subordinates) {
            importance += dfs(subID);
        }
        
        return importance;
    }
}
```
