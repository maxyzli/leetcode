# Find the Difference

## Solution 1

```java
/**
 * Question   : 389. Find the Difference
 * Complexity : Time: O(s+t) ; Space: O(1)
 * Topics     : Bit
 */
class Solution {
    public char findTheDifference(String s, String t) {
        if (s.length() == 0) {
            return t.charAt(0);
        }

        int diff = s.charAt(0) - 'a';

        for (int i = 1; i < s.length(); i++) {
            diff ^= (s.charAt(i) - 'a');
        }

        for (int i = 0; i < t.length(); i++) {
            diff ^= (t.charAt(i) - 'a');
        }

        return (char)('a' + diff);
    }
}
```
