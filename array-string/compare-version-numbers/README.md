# Compare Version Numbers

## Solution 1

```java
/**
 * Question   : 165. Compare Version Numbers
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : string
 */
class Solution {
    public int compareVersion(String version1, String version2) {
        int v1Begin = 0;
        int v2Begin = 0;

        while (v1Begin < version1.length() || v2Begin < version2.length()) {
            int num1 = 0;
            int num2 = 0;

            // Get a number from version1.
            if (v1Begin < version1.length()) {
                if (version1.charAt(v1Begin) == '.') {
                    v1Begin++;
                }
                int v1End = v1Begin;
                while (v1End < version1.length() && version1.charAt(v1End) != '.') {
                    v1End++;
                }
                num1 = Integer.valueOf(version1.substring(v1Begin, v1End));
                v1Begin = v1End;
            }

            // Get a number from version2.
            if (v2Begin < version2.length()) {
                if (version2.charAt(v2Begin) == '.') {
                    v2Begin++;
                }
                int v2End = v2Begin;
                while (v2End < version2.length() && version2.charAt(v2End) != '.') {
                    v2End++;
                }
                num2 = Integer.valueOf(version2.substring(v2Begin, v2End));
                v2Begin = v2End;
            }

            if (num1 > num2) {
                return 1;
            }
            if (num2 > num1) {
                return -1;
            }
        }

        return 0;
    }
}
```

## Solution 2

```java
/**
 * Question   : 165. Compare Version Numbers
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : string
 */
class Solution {
    public int compareVersion(String version1, String version2) {
        int i1 = 0;
        int i2 = 0;

        while (i1 < version1.length() || i2 < version2.length()) {
            int num1 = 0;
            int num2 = 0;

            // Get a number from version1.
            if (i1 < version1.length()) {
                if (version1.charAt(i1) == '.') {
                    i1++;
                }
                while (i1 < version1.length() && version1.charAt(i1) != '.') {
                    num1 = num1 * 10 + version1.charAt(i1) - '0';
                    i1++;
                }
            }

            // Get a number from version2.
            if (i2 < version2.length()) {
                if (version2.charAt(i2) == '.') {
                    i2++;
                }
                while (i2 < version2.length() && version2.charAt(i2) != '.') {
                    num2 = num2 * 10 + version2.charAt(i2) - '0';
                    i2++;
                }
            }

            if (num1 > num2) {
                return 1;
            }
            if (num2 > num1) {
                return -1;
            }
        }

        return 0;
    }
}
```
