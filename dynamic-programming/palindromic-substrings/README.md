# Palindromic Substrings

## Solution 1: DP

```java
// TC: O(n^2)
// SC: O(n^2)
public class Solution {
    public int countSubstrings(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }

        int n = s.length();

        boolean[][] dp = new boolean[n][n];
        int count = 0;

        for (int len = 1; len <= n; len++) {
            for (int i = 0; i < n - len + 1; i++) {
                int j = i + len - 1;

                if (len == 1) {
                    dp[i][j] = true;
                    count++;
                } else if (len == 2) {
                    if (s.charAt(i) == s.charAt(j)) {
                        dp[i][j] = true;
                        count++;
                    }
                } else { // len >= 3
                    if (s.charAt(i) == s.charAt(j) && dp[i + 1][j - 1]) {
                        dp[i][j] = true;
                        count++;
                    }
                }
            }
        }

        return count;
    }
}
```

## Solution 2: Expending

```java
// TC: O(n)
// SC: O(1)
class Solution {
    public int countSubstrings(String s) {
         if (s == null || s.length() == 0) {
            return 0;
        }

        int count = 0;

        for (int i = 0; i < s.length(); i++) {
            int lo = i;
            int hi = i;
            while (lo >= 0 && hi < s.length() && s.charAt(lo) == s.charAt(hi)) {
                count++;
                lo--;
                hi++;
            }

            lo = i;
            hi = i + 1;
            while (lo >= 0 && hi < s.length() && s.charAt(lo) == s.charAt(hi)) {
                count++;
                lo--;
                hi++;
            }
        }

        return count;
    }
}
```
