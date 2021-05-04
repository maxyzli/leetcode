# Reverse String II

## Solution 1

```java
/**
 * Question   : 541. Reverse String II
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : String
 */
class Solution {
    public String reverseStr(String s, int k) {
        StringBuilder sb = new StringBuilder(s);

        int i = 0;

        while (i < sb.length()) {
            int j = i + k - 1;

            // If there are fewer than k characters left, reverse all of them.
            if (j >= sb.length()) {
                reverse(sb, i, sb.length() - 1);
                break;
            }

            // reverse the first k
            reverse(sb, i, j);

            // for every 2k characters
            i += (2 * k);
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
