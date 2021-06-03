# Longest Substring Without Repeating Characters

## Solution 1

Sliding Window

```java
/**
 * Question   : 3. Longest Substring Without Repeating Characters
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Sliding Window
 */
class Solution {
    public int lengthOfLongestSubstring(String s) {
        Set<Character> window = new HashSet<>();

        int left = 0;
        int right = 0;
        int longest = 0;

        while (right < s.length()) {
            Character c = s.charAt(right++);

            while (window.contains(c)) {
                Character charToRemove = s.charAt(left++);
                if (window.contains(charToRemove)) {
                    window.remove(charToRemove);
                }
            }

            window.add(c);
            longest = Math.max(longest, right - left);
        }

        return longest;
    }
}
```
