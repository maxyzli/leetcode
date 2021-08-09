# Minimum Window Substring

## Solution 1

Sliding Window

Note: Do not compare two Integer types with `==`

```java
/**
 * Question   : 76. Minimum Window Substring
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Sliding Window
 */
class Solution {
    public String minWindow(String s, String t) {
        Map<Character, Integer> window = new HashMap<>();
        Map<Character, Integer> need = new HashMap<>();

        for (int i = 0; i < t.length(); i++) {
            char c = t.charAt(i);
            need.put(c, need.getOrDefault(c, 0) + 1);
        }

        int left = 0;
        int right = 0;
        int require = need.size();
        String substring = "";

        while (right < s.length()) {
            char curr = s.charAt(right++);

            window.put(curr, window.getOrDefault(curr, 0) + 1);
            if (window.get(curr).equals(need.get(curr))) {
                require--;
            }

            while (require == 0) {
                if (substring == "" || substring.length() > right - left) {
                    substring = s.substring(left, right);
                }

                char charToRemove = s.charAt(left++);

                if (window.get(charToRemove).equals(need.get(charToRemove))) {
                    require++;
                }
                window.put(charToRemove, window.get(charToRemove) - 1);
            }
        }

        return substring;
    }
}
```
