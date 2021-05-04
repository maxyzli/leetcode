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

        int end = s.length() - 1;

        // Skip white spaces.
        while (end >= 0 && s.charAt(end) == ' ') {
            end--;
        }

        int start = end;
        while (start >= 0 && s.charAt(start) != ' ') {
            start--;
        }

        return end - start;
    }
}
```
