# Length of Last Word

## Solution 1

```java
/**
 * Question   : 58. Length of Last Word
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : string
 */
class Solution {
    public int lengthOfLastWord(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }

        int idx = s.length() - 1;

        // Skip white spaces.
        while (idx >= 0 && s.charAt(idx) == ' ') {
            idx--;
        }

        int count = 0;
        while (idx >= 0 && s.charAt(idx) != ' ') {
            count++;
            idx--;
        }

        return count;
    }
}
```
