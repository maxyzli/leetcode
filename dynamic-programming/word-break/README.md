# Word Break

## Solution 1

DFS (Time Limit Exceeded)

```java
/**
 * Question   : 139. Word Break
 * Complexity : Time: O(n^h) ; Space: O(h)
 * Topics     : DFS, DP
 */
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        int sIdx = 0;
        return wordBreakUtil(s, wordDict, sIdx);
    }

    private boolean wordBreakUtil(String s, List<String> wordDict, int sIdx) {
        if (sIdx == s.length()) {
            return true;
        }

        boolean possible = false;
        for (int i = 0; i < wordDict.size(); i++) {
            String word = wordDict.get(i);
            int wordLen = word.length();
            if (sIdx + wordLen <= s.length() && s.substring(sIdx, sIdx + wordLen).equals(word)) {
                possible = possible || wordBreakUtil(s, wordDict, sIdx + wordLen);
            }
        }

        return possible;
    }
}
```

## Solution 2

DP

```java
/**
 * Question   : 139. Word Break
 * Complexity : Time: O(n*len(wordDict)) ; Space: O(n)
 * Topics     : DFS, DP
 */
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        int n = s.length();

        // dp[i]: if we can generate s.substring(0, i) using wordDict.
        boolean[] dp = new boolean[n + 1];
        dp[0] = true;

        for (int beginIdx = 0; beginIdx < n; beginIdx++) {
            for (int j = 0; j < wordDict.size(); j++) {
                String word = wordDict.get(j);
                int endIdx = beginIdx + word.length();
                if (endIdx <= s.length()) {
                    dp[endIdx] = dp[endIdx] || (dp[beginIdx] && s.substring(beginIdx, endIdx).equals(word));
                }
            }
        }

        return dp[n];
    }
}
```
