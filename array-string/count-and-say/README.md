# Count and Say

## Solution 1

```java
/**
 * Question   : 38. Count and Say
 * Complexity : Time: O(n^2) ; Space: O(n)
 * Topics     : String
 */
class Solution {
    public String countAndSay(int n) {
        if (n == 1) {
            return "1";
        }

        String s = countAndSay(n - 1);

        StringBuilder sb = new StringBuilder();
        char pre = s.charAt(0);
        int counter = 1;
        for (int i = 1; i < s.length(); i++) {
            char curr = s.charAt(i);
            if (pre != curr) {
                sb.append(counter);
                sb.append(pre);
                // Reset
                pre = curr;
                counter = 1;
            } else {
                counter++;
            }
        }
        sb.append(counter);
        sb.append(pre);

        return sb.toString();
    }
}
```
