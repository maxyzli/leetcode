# Longest Palindromic Substring

## Solution 1

Expand From the Center

```java
public class Solution {
    public int findLongest(String str) {
        if (str == null || str == "") {
            return 0;
        }
        if (str.length() == 1) {
            return 1;
        }

        int maxLength = 1;

        for (int i = 0; i < str.length(); i++) {
            Math.max(
                    maxLength,
                    Math.max(checkPalindrome(str, i, i), checkPalindrome(str, i, i + 1))
            );
        }

        return maxLength;
    }

    private int checkPalindrome(String str, int left, int right) {
        int length = 0;
        while (left >= 0 && right < str.length()) {
            if (str.charAt(left) != str.charAt(right)) {
                break;
            }
            length = right - left + 1;
            left--;
            right++;
        }
        return length;
    }
}
```

## Solution 2

DP

```java
/**
 * Question   : Longest Palindromic Substring
 * Complexity : Time: O(n^2) ; Space: O(n^2)
 * Topics     : DP
 * Date       : 2021/01/05
 */
public class Solution {
    public String longestPalindrome(String s) {
        if (s.length() <= 1) {
            return s;
        }

        // [start] - [end]
        int len = s.length();
        boolean[][] m = new boolean[len][len];

        int subStringStart = 0, maxLength = 1;

        // Initialization.
        for (int i = 0; i < len; i++) {
            m[i][i] = true;
            if (i + 1 < len && s.charAt(i) == s.charAt(i + 1)) {
                m[i][i + 1] = true;
                subStringStart = i;
                maxLength = 2;
            }
        }

        for (int length = 3; length <= len; length++) {
            for (int start = 0; start < len; start++) {
                int end = start + length - 1;
                if (end >= len) {
                    break;
                }
                if (s.charAt(start) == s.charAt(end) && m[start + 1][end - 1] == true) {
                    m[start][end] = true;
                    if (length > maxLength) {
                        subStringStart = start;
                        maxLength = length;
                    }
                }
            }
        }

        return s.substring(subStringStart, subStringStart + maxLength);
    }
}
```
