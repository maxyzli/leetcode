# Longest Palindromic Subsequence

## Solution 1

Brute Force (Time Limit Exceeded)

```java
/**
 * Question   : 5. Longest Palindromic Substring
 * Complexity : Time: O(n^3) ; Space: O(1)
 * Topics     : DP
 */
class Solution {
    public String longestPalindrome(String s) {
        if (s == null || s.length() == 0) {
            return "";
        }

        int n = s.length();
        int maxLength = 0;
        int beginIndex = 0;

        for (int i = 0; i < n; i++) {
            for (int j = i; j < n; j++) {
                if (isPalindrome(s, i, j)) {
                    if (j - i + 1 > maxLength) {
                        maxLength = j - i + 1;
                        beginIndex = i;
                    }
                }
            }
        }

        return s.substring(beginIndex, beginIndex + maxLength);
    }

    private boolean isPalindrome(String s, int i, int j) {
        while (i < j) {
            if (s.charAt(i) != s.charAt(j)) {
                return false;
            }
            i++;
            j--;
        }
        return true;
    }
}
```

## Solution 2

DP

```java
/**
 * Question   : 5. Longest Palindromic Substring
 * Complexity : Time: O(n^2) ; Space: O(n^2)
 * Topics     : DP
 */
class Solution {
    public String longestPalindrome(String s) {
        if (s == null || s.length() == 0) {
            return "";
        }

        int n = s.length();

        boolean[][] memo = new boolean[n][n];
        int maxLength = 1;
        int beginIndex = 0;

        for (int len = 1; len <= n; len++) {
            for (int i = 0; i < n - len + 1; i++) {
                int j = i + len - 1;

                if (len == 1) {
                    memo[i][j] = true;
                } else if (len == 2) {
                    if (s.charAt(i) == s.charAt(j)) {
                        maxLength = 2;
                        beginIndex = i;
                        memo[i][j] = true;
                    }
                } else {
                    if (s.charAt(i) == s.charAt(j) && memo[i + 1][j - 1]) {
                        maxLength = len;
                        beginIndex = i;
                        memo[i][j] = true;
                    }
                }
            }
        }

        return s.substring(beginIndex, beginIndex + maxLength);
    }
}
```

## Solution 3

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
