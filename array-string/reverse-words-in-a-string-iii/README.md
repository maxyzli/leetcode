# Reverse Words in a String III

## Solution 1

```java
/**
 * Question   : 557. Reverse Words in a String III
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : String
 */
class Solution {
    public String reverseWords(String s) {
        if (s == null || s.length() == 0) {
            return s;
        }

        StringBuilder sb = new StringBuilder(s);

        int n = sb.length();
        int i = 0;
        int j = 0;

        while (j < n) {
            // Find first space.
            while (j < n && sb.charAt(j) != ' ') {
                j++;
            }

            reverse(sb, i, j - 1);

            // Find next start character.
            while (j < n && sb.charAt(j) == ' ') {
                j++;
            }

            i = j;
        }

        return sb.toString();
    }

    private void reverse(StringBuilder sb, int i, int j) {
        while (i < j) {
            char temp = sb.charAt(i);
            sb.setCharAt(i, sb.charAt(j));
            sb.setCharAt(j, temp);
            i++;
            j--;   
        }
    }
}
```
