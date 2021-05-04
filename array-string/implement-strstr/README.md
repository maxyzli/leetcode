# Implement strStr()

## Solution 1

```java
/**
 * Question   : 28. Implement strStr()
 * Complexity : Time: O(n*m) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public int strStr(String haystack, String needle) {
        if (needle == "") {
            return 0;
        }
        if (haystack == "") {
            return -1;
        }

        int needleLen = needle.length();

        for (int i = 0; i <= haystack.length() - needleLen; i++) {
            if (haystack.substring(i, i + needleLen).equals(needle)) {
                return i;
            }
        }

        return -1;
    }
}
```
