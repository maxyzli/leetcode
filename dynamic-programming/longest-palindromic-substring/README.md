# Longest Palindromic Substring

## Solution 1: Brute Force (Time Limit Exceeded)

```java
// TC: O(n^3)
// SC: O(1)
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

## Solution 2: DP

```java
// TC: O(n^2)
// SC: O(n^2)
class Solution {
    public String longestPalindrome(String s) {
        if (s == null || s.length() == 0) {
            return "";
        }

        int n = s.length();

        boolean[][] dp = new boolean[n][n];
        int maxLength = 1;
        int beginIndex = 0;

        for (int len = 1; len <= n; len++) {
            for (int i = 0; i < n - len + 1; i++) {
                int j = i + len - 1;

                if (len == 1) {
                    dp[i][j] = true;
                } else if (len == 2) {
                    if (s.charAt(i) == s.charAt(j)) {
                        maxLength = 2;
                        beginIndex = i;
                        dp[i][j] = true;
                    }
                } else {
                    if (s.charAt(i) == s.charAt(j) && dp[i + 1][j - 1]) {
                        maxLength = len;
                        beginIndex = i;
                        dp[i][j] = true;
                    }
                }
            }
        }

        return s.substring(beginIndex, beginIndex + maxLength);
    }
}
```

## Solution 3: Expand From the Center

```java
// TC: O(n)
// SC: O(1)
class Solution {
    public String longestPalindrome(String s) {
        if (s == null || s.length() == 0) {
            return "";
        }

        int maxLen = 0;
        int resLo = 0;
        int resHi = 0;

        for (int i = 0; i < s.length(); i++) {
            int lo = i;
            int hi = i;
            while (lo >= 0 && hi < s.length() && s.charAt(lo) == s.charAt(hi)) {
                if (hi - lo + 1 > maxLen) {
                    maxLen = hi - lo + 1;
                    resLo = lo;
                    resHi = hi;
                }
                lo--;
                hi++;
            }

            lo = i;
            hi = i + 1;
            while (lo >= 0 && hi < s.length() && s.charAt(lo) == s.charAt(hi)) {
                if (hi - lo + 1 > maxLen) {
                    maxLen = hi - lo + 1;
                    resLo = lo;
                    resHi = hi;
                }
                lo--;
                hi++;
            }
        }

        return s.substring(resLo, resHi + 1);
    }
}
```
