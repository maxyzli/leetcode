# Palindrome Partitioning

## Solution 1

DFS

```java
/**
 * Question   : 131. Palindrome Partitioning
 * Complexity : Time: O(n^3) ; Space: O(n)
 * Topics     : DFS
 */
class Solution {
    public List<List<String>> partition(String s) {
        if (s == null || s.length() == 0) {
            return new ArrayList<>();
        }

        List<List<String>> res = new ArrayList<>();
        List<String> list = new ArrayList<>();
        int beginIndex = 0;

        partitionUtil(s, beginIndex, list, res);

        return res;
    }

    private void partitionUtil(String s, int beginIndex, List<String> list, List<List<String>> res) {
        if (beginIndex == s.length()) {
            res.add(new ArrayList<>(list));
            return;
        }

        for (int endIndex = beginIndex + 1; endIndex <= s.length(); endIndex++) { // O(n)
            if (isPalindrome(s, beginIndex, endIndex - 1)) { // O(n)
                list.add(s.substring(beginIndex, endIndex));
                partitionUtil(s, endIndex, list, res);
                list.remove(list.size() - 1);
            }
        }
    }

    private boolean isPalindrome(String s, int left, int right) {
        if (s == "") {
            return true;
        }

        while (left < right) {
            if (s.charAt(left) != s.charAt(right)) {
                return false;
            }
            left++;
            right--;
        }

        return true;
    }
}
```

## Solution 2

DFS + DP

```java
import java.util.*;

/**
 * Question   : 131. Palindrome Partitioning
 * Complexity : Time: O(n^2) ; Space: O(n^2)
 * Topics     : DP
 */
class Solution {
    boolean[][] dp;

    public List<List<String>> partition(String s) {
        if (s == null || s.length() == 0) {
            return new ArrayList<>();
        }

        dp = new boolean[s.length()][s.length()];
        checkPalindrome(s, dp);

        List<List<String>> res = new ArrayList<>();
        List<String> list = new ArrayList<>();
        int beginIndex = 0;

        partitionUtil(s, beginIndex, list, res);

        return res;
    }

    private void partitionUtil(String s, int beginIndex, List<String> list, List<List<String>> res) {
        if (beginIndex == s.length()) {
            res.add(new ArrayList<>(list));
            return;
        }

        for (int endIndex = beginIndex + 1; endIndex <= s.length(); endIndex++) { // O(n)
            if (dp[beginIndex][endIndex - 1]) { // O(1)
                list.add(s.substring(beginIndex, endIndex));
                partitionUtil(s, endIndex, list, res);
                list.remove(list.size() - 1);
            }
        }
    }

    public void checkPalindrome(String s, boolean[][] dp) {
        if (s == null || s.length() == 0) {
            return;
        }

        int n = s.length();

        for (int len = 1; len <= n; len++) {
            for (int i = 0; i < n - len + 1; i++) {
                int j = i + len - 1;

                if (len == 1) {
                    dp[i][j] = true;
                } else if (len == 2) {
                    if (s.charAt(i) == s.charAt(j)) {
                        dp[i][j] = true;
                    }
                } else { // len >= 3
                    if (s.charAt(i) == s.charAt(j) && dp[i + 1][j - 1]) {
                        dp[i][j] = true;
                    }
                }
            }
        }
    }
}
```
