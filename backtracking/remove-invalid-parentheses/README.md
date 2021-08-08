# Remove Invalid Parentheses

## Solution 1

```java
/**
 * Question   : 301. Remove Invalid Parentheses
 * Complexity : Time: O(2^n) ; Space: O(n)
 * Topics     : Backtracking
 */
class Solution {
    Set<String> set;
    
    public List<String> removeInvalidParentheses(String s) {
        if (s == null || s.length() == 0) {
            return new LinkedList();
        }
        
        set = new HashSet<>();
        
        int leftRemove = 0;
        int rightRemove = 0;
        
        // Calculate how many left and right brackets needs to remove.
        for (char c : s.toCharArray()) {
            if (c == '(') {
                leftRemove++;
            }
            if (c == ')') {
                if (leftRemove == 0) {
                    rightRemove++;
                } else {
                    leftRemove--;
                }
            }
        }
        
        StringBuilder sb = new StringBuilder();
        dfs(s, 0, 0, 0, leftRemove, rightRemove, sb);
        
        return new ArrayList(set);
    }
    
    private void dfs(
        String s, 
        int index,
        int leftCount,
        int rightCount,
        int leftRemove, 
        int rightRemove, 
        StringBuilder sb
    ) {
        if (index == s.length()) {
            if (leftRemove == 0 && rightRemove == 0) {
                set.add(sb.toString());
            }
            return;
        }
        
        char c = s.charAt(index);
        
        if (c == '(' && leftRemove > 0) {
            dfs(s, index + 1, leftCount, rightCount, leftRemove - 1, rightRemove, sb);
        }
        if (c == ')' && rightRemove > 0) {
            dfs(s, index + 1, leftCount, rightCount, leftRemove, rightRemove - 1, sb);
        }
        
        // If right brackets are more than left brackets, it's impossible to find a solution.
        if (rightCount > leftCount) {
            return;
        }
        
        sb.append(c);
        
        if (c == '(') {
            dfs(s, index + 1, leftCount + 1, rightCount, leftRemove, rightRemove, sb);       
        } else if (c == ')') {
            dfs(s, index + 1, leftCount, rightCount + 1, leftRemove, rightRemove, sb);
        } else { 
            // lowercase English letters
            dfs(s, index + 1, leftCount, rightCount, leftRemove, rightRemove, sb);      
        }

        sb.deleteCharAt(sb.length() - 1);
    }
}
```
