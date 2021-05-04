# Repeated Substring Pattern

## Solution 1

Brute Force

```java
/**
 * Question   : 459. Repeated Substring Pattern
 * Complexity : Time: O(n*m) ; Space: O(1)
 * Topics     : String
 */
class Solution {
    public boolean repeatedSubstringPattern(String s) {
        if (s == null || s.length() == 0) {
            return true;
        }

        int n = s.length();

        for (int len = 1; len <= n / 2; len++) {
           // Make sure the length of the string is the multiple of len.
            if (n % len != 0) {
                continue;
            }gma

            String sub = s.substring(0, len);

            int i = 0;
            while (i < n) {
                if ((i + len > n) || (!s.substring(i, i + len).equals(sub))) {
                    break;
                }
                i += len;
            }

            if (i == n) {
                return true;
            }
        }

        return false;
    }
}
```

## Solution 2

Two Pointers

```java
/**
 * Question   : 459. Repeated Substring Pattern
 * Complexity : Time: O(n*m) ; Space: O(1)
 * Topics     : String
 */
class Solution {
    public boolean repeatedSubstringPattern(String s) {
        if (s == null || s.length() == 0) {
            return true;
        }

        int n = s.length();

        for (int len = 1; len <= n / 2; len++) {
            // Make sure the length of the string is the multiple of len.
            if (n % len != 0) {
                continue;
            }
            boolean matched = true;
            int i = 0;
            for (int j = len; j < n; j++) {
                if (s.charAt(i) != s.charAt(j)) {
                    matched = false;
                    break;
                }
                i++;

            }
            if (matched) {
                return true;
            }
        }

        return false;
    }
}
```
