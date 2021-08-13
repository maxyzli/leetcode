# Restore IP Addresses

## Solution 1

```java
/**
 * Question   : 93. Restore IP Addresses
 * Complexity : Time: O(3^SEG_COUNT) ; Space: O(SEG_COUNT)
 * Topics     : Backtracking
 */
/**
 * Question   : 93. Restore IP Addresses
 * Complexity : Time: O(3^4) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public List<String> restoreIpAddresses(String s) {
        if (s == null || s.length() == 0) {
            return new LinkedList<>();
        }

        List<String> res = new LinkedList<>();
        List<String> list = new LinkedList<>();
        int startIdx = 0;
        
        dfs(s, startIdx, list, res);
        
        return res;
    }
    
    private void dfs(String s, int startIdx, List<String> list, List<String> res) {
        if (list.size() == 4) {
            if (startIdx == s.length()) {
                res.add(String.join(".", list));
            }   
            return;
        }
        
        for (int endIdx = startIdx; endIdx < startIdx + 3; endIdx++) {
            if (endIdx >= s.length()) {
                break;
            }
            if (isValid(s, startIdx, endIdx)) {
                list.add(s.substring(startIdx, endIdx + 1));
                dfs(s, endIdx + 1, list, res);
                list.remove(list.size() - 1);
            }
        }
    }
    
    private boolean isValid(String s, int startIdx, int endIdx) {
        // check leading zero.
        if (startIdx != endIdx && s.charAt(startIdx) == '0') {
            return false;
        }
        
        int num = 0;
        for (int i = startIdx; i <= endIdx; i++) {
            num = num * 10 + (s.charAt(i) - '0');
        }
        
        if (num > 255) {
            return false;
        }
        
        return true;
    }
}
```
