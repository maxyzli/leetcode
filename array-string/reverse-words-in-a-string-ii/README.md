# Reverse Words in a String II

## Solution 1

```java
/**
 * Question   : 186. Reverse Words in a String II
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : String
 */
class Solution {
    public void reverseWords(char[] s) {
        if (s == null || s.length == 0) {
            return;
        }
        
        int slow = 0;
        int fast = 0;
        
        while (fast < s.length) {
            while (fast < s.length && s[fast] != ' ') {
                fast++;
            }
            reverse(s, slow, fast - 1);
            // point to next start word
            fast++;
            slow = fast;
        }
        // reverse the last word
        reverse(s, slow, fast - 1);
        // reverse the entire array
        reverse(s, 0, s.length - 1);
    }
    
    public void reverse(char[] s, int start, int end) {
        while (start < end) {
            char temp = s[start];
            s[start] = s[end];
            s[end] = temp;
            start++;
            end--;
        }
    }
}
```
