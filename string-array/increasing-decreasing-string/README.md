# Increasing Decreasing String 

## Solution 1

```java
/**
 * Question   : 1370. Increasing Decreasing String
 * Complexity : Time: O(m*n) ; Space: O(1)
 * Topics     : String
 */
class Solution {
    public String sortString(String s) {
        if (s == null || s.length() == 0) {
            return "";
        }

        int[] freq = new int[26]; // Space: O(1)
        int n = s.length();

        for (int i = 0; i < n; i++) { // Time: O(n)
            freq[s.charAt(i) - 'a']++;
        }

        StringBuilder sb = new StringBuilder();

        while (sb.length() < n) { // Time: (n)
            // 1. Pick the smallest character from s and append it to the result.
            for (int j = 0; j < 26; j++) {
                char c = (char) (j + 'a');
                if (freq[j] > 0) {
                    sb.append(c);
                    freq[j]--;
                    break;
                }
            }

            // 2. Pick the smallest character from s which is greater than
            // the last appended character to the result and append it.
            boolean repeat = true;
            while (repeat) {
                boolean flag = false;
                for (int j = 0; j < 26; j++) {
                    char c = (char) (j + 'a');
                    if (freq[j] > 0 && c > sb.charAt(sb.length() - 1)) {
                        sb.append(c);
                        freq[j]--;
                        flag = true;
                    }
                }
                // 3. Repeat step 2 until you cannot pick more characters.
                repeat = flag;
            }

            // 4. Pick the largest character from s and append it to the result.
            for (int j = 25; j >= 0; j--) {
                char c = (char) (j + 'a');
                if (freq[j] > 0) {
                    sb.append(c);
                    freq[j]--;
                    break;
                }
            }

            // 5. Pick the largest character from s which is smaller
            // than the last appended character to the result and append it.
            repeat = true;
            while (repeat) {
                boolean flag = false;
                for (int j = 25; j >= 0; j--) {
                    char c = (char) (j + 'a');
                    if (freq[j] > 0 && c < sb.charAt(sb.length() - 1)) {
                        sb.append(c);
                        freq[j]--;
                        flag = true;
                    }
                }
                // 6. Repeat step 5 until you cannot pick more characters.
                repeat = flag;
            }
        }

        return sb.toString();
    }
}
```

## Solution 2

Combine Steps Together

```java
/**
 * Question   : 1370. Increasing Decreasing String
 * Complexity : Time: O(m*n) ; Space: O(1)
 * Topics     : String
 */
class Solution {
    public String sortString(String s) {
        if (s == null || s.length() == 0) {
            return "";
        }

        int[] freq = new int[26]; // Space: O(1)
        int n = s.length();

        for (int i = 0; i < n; i++) { // Time: O(n)
            freq[s.charAt(i) - 'a']++;
        }

        StringBuilder sb = new StringBuilder();

        while (sb.length() < n) { // Time: (n)
            // 1. Pick the smallest character from s and append it to the result.
            // 2. Pick the smallest character from s which is greater than
            // the last appended character to the result and append it.
            // 3. Repeat step 2 until you cannot pick more characters.
            for (int j = 0; j < 26; j++) {
                char c = (char) (j + 'a');
                if (freq[j] > 0) {
                    sb.append(c);
                    freq[j]--;
                }
            }

            // 4. Pick the largest character from s and append it to the result.
            // 5. Pick the largest character from s which is smaller
            // than the last appended character to the result and append it.
            // 6. Repeat step 5 until you cannot pick more characters.
            for (int j = 25; j >= 0; j--) {
                char c = (char) (j + 'a');
                if (freq[j] > 0) {
                    sb.append(c);
                    freq[j]--;
                }
            }
        }

        return sb.toString();
    }
}
```