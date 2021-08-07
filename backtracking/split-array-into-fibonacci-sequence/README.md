# Split Array into Fibonacci Sequence

## Solution 1

Backtracking

```java
/**
 * Question   : 842. Split Array into Fibonacci Sequence
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Backtracking
 */
class Solution {
    List<Integer> res;
    
    public List<Integer> splitIntoFibonacci(String num) {
        List<Integer> temp = new LinkedList<>();
        int beginIdx = 0;      
        dfs(num, beginIdx, temp);
        return res == null ? new LinkedList<>() : res;
    }

    private boolean dfs(String num, int beginIdx, List<Integer> temp) {
        if (beginIdx == num.length() && temp.size() > 2) {
            res = new LinkedList(temp);    
            return true;
        }
        
        for (int endIdx = beginIdx + 1; endIdx <= num.length(); endIdx++) {
            String candidateStr = num.substring(beginIdx, endIdx);
            // avoid leading zeroes
            if (candidateStr.length() > 1 && candidateStr.charAt(0) == '0') {
                break;
            }
            // avoid integer overflow
            if (Long.valueOf(candidateStr) > Integer.MAX_VALUE) {
                break;
            }
            
            int candidate = Integer.valueOf(candidateStr);
            
            if (temp.size() >= 2) {
                int prevTwoSum = temp.get(temp.size() - 1) + temp.get(temp.size() - 2);
                if (prevTwoSum > candidate) {
                    continue;
                }
                if (prevTwoSum < candidate) {
                    break;
                }   
            }

            temp.add(candidate);
            if (dfs(num, endIdx, temp)) {
                return true;
            }
            temp.remove(temp.size() - 1);
        }
        
        return false;
    }
}
```
